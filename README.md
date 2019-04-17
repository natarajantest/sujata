import java.util.concurrent.TimeUnit;

import org.openqa.selenium.By;
import org.openqa.selenium.By.ById;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.support.ui.Select;

public class Assignment {

	public static void main(String[] args) throws InterruptedException {

		WebDriver driver = new ChromeDriver();
		driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
		driver.manage().window().maximize();
		driver.get("https://demo.openemr.io/d/openemr/interface/login/login.php?site=default");

		// login
		driver.findElement(By.id("authUser")).clear();
		driver.findElement(By.id("authUser")).sendKeys("admin");
		driver.findElement(By.id("clearPass")).clear();
		driver.findElement(By.id("clearPass")).sendKeys("pass");
		driver.findElement(By.xpath("//i[@class='fa fa-sign-in']")).click();

		// navigate
		Actions act = new Actions(driver);
		act.moveToElement(driver.findElement(By.xpath("//div[text()='Patient/Client']"))).build().perform();
		act.click(driver.findElement(By.xpath("//div[text()='New/Search']"))).build().perform();

		// switchwindow
		driver.switchTo().frame(driver.findElement(By.xpath("//iframe[@name='pat']")));

		// fname & lname
		driver.findElement(By.xpath("//input[@id='form_fname']")).sendKeys("admin");
		driver.findElement(By.id("form_lname")).sendKeys("123");

		// DOB
		driver.findElement(By.id("form_DOB")).click();
		driver.findElement(By.xpath("//div[text()='17']")).click();

		// sex
		Select s = new Select(driver.findElement(By.id("form_sex")));
		s.selectByIndex(1);

		//create new patient
		driver.findElement(By.id("create")).click();
		driver.switchTo().defaultContent();
		
		driver.switchTo().frame(driver.findElement(By.xpath("//iframe[@class='embed-responsive-item modalIframe']")));
		driver.findElement(By.xpath("//input[@value='Confirm Create New Patient']")).click();
		
		Thread.sleep(8000);
		driver.switchTo().alert().accept();
		
	    driver.findElement(By.xpath("//div[@class='closeDlgIframe']")).click();
		   // driver.switchTo().frame(driver.findElement(By.name("timeout")));
		   // Actions act1=new Actions(driver);
		    act.moveToElement(driver.findElement(By.xpath("//div[@class='menuSection userSection']"))).build().perform();
		    driver.findElement(By.xpath("//ul//li[text()='Logout']")).click();

		    Thread.sleep(3000);
		    driver.quit();
		}

	}

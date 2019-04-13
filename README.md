package initialize;

import java.util.concurrent.TimeUnit;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.Select;
import org.openqa.selenium.support.ui.WebDriverWait;

public class SpiceJet {

	public static void main(String[] args) throws InterruptedException {
		WebDriver driver = new ChromeDriver();
		WebDriverWait wait=new WebDriverWait(driver,30);
		driver.manage().window().maximize();
		driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
		driver.get("http://www.spicejet.com");
		driver.findElement(By.xpath("(//span[@class='red-arrow-btn'])[1]")).click();
		driver.findElement(By.linkText("Mumbai (BOM)")).click();

		driver.findElement(By.xpath("(//span[@class='red-arrow-btn'])[2]")).click();
		driver.findElement(By.linkText("Dehradun (DED)")).click();

		Actions act = new Actions(driver);
		act.moveToElement(driver.findElement(By.linkText("19"))).build().perform();
		driver.findElement(By.linkText("19")).click();
		
		Thread.sleep(3000);
//		act.moveToElement(driver.findElement(By.linkText("25"))).build().perform(); //	driver.findElement(By.linkText("25")).click();

	driver.findElement(By.className("paxinfo")).click();
	for(int i=0;i<=3;i++)
	{  
	driver.findElement(By.id("hrefIncAdt")).click();
	i=i+1;
	}	
	Thread.sleep(3000);
	driver.findElement(By.id("btnclosepaxoption")).click();
	Select sc=new Select(driver.findElement(By.id("ctl00_mainContent_DropDownListCurrency"))); sc.selectByValue("AED"); Thread.sleep(3000); driver.findElement(By.id("ctl00_mainContent_btn_FindFlights")).click();

	}
	}

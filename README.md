# dd_test_core
This includes initialization of webdriver, excel files and properties files
// It contains code for initialization

package dd_core;

import java.io.FileInputStream;
import java.io.IOException;
import java.util.Properties;
//import java.util.concurrent.TimeUnit;
import java.util.concurrent.TimeUnit;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterSuite;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeSuite;
import org.testng.annotations.BeforeTest;

import dd_utils.Xls_Reader;

public class TestCore
{
	
	
	public static Properties config = new Properties();
	public static Properties object = new Properties();
	public static Xls_Reader excel = null;
	public static WebDriver driver = null;
	
	
	@BeforeSuite
	public static void init() throws IOException
	{
		System.out.println("inside init method");
		if(driver == null)
		{
			
			FileInputStream fis = new FileInputStream(System.getProperty("user.dir")+"//src//dd_properties//config.properties");
			config.load(fis);
			
			fis = new FileInputStream(System.getProperty("user.dir")+"//src//dd_properties//object.properties");
			object.load(fis);
			 
			excel = new Xls_Reader(System.getProperty("user.dir")+"//src//dd_properties//Testdata.xlsx");
			
			
			
			     if(config.getProperty("browser").equals("Chrome"))
			     {
			    	 
			    	 System.setProperty("webdriver.chrome.driver", "chromedriver.exe");
					 driver = new ChromeDriver();
			    	 
			     }
			
			driver.get(config.getProperty("testsite"));
			driver.manage().timeouts().implicitlyWait(30L, TimeUnit.SECONDS);
			
		}

				
	}
	
	
	
	@AfterSuite
	public static void QuitDriver()
	{
		driver.close();
		driver.quit();
	}
	
	
	
	
	
	
   
}

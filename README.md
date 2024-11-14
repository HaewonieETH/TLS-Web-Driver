![Logo](http://francky.me/images/quora001.png)

## Getting Started ##
This driver currently can be downloaded as an executable. Start the web driver service with:

	./TLS.WebDriver.exe --urls=http://localhost:4723/

 After it has started, it can be used via WebDriver clients such as for example:

* [Appium.WebDriver](https://www.nuget.org/packages/Appium.WebDriver)
* [Selenium.WebDriver](https://www.nuget.org/packages/Selenium.WebDriver)
* [Selenium.WebDriver](https://www.npmjs.com/package/webdriverio)

Using the [Appium.WebDriver](https://www.nuget.org/packages/Appium.WebDriver) C# client:
	using OpenQA.Selenium.Appium.Windows;

	public class FlaUIDriverOptions : AppiumOptions
  	{
      public static FlaUIDriverOptions ForApp(string path)
      {
          return new FlaUIDriverOptions()
          {
              PlatformName = "windows",
              AutomationName = "flaui",
              App = path
          };
      }
  	}

	var driver = new WindowsDriver(new Uri("http://localhost:4723"), FlaUIDriverOptions.ForApp("C:\\YourApp.exe"))

 Using the [Selenium.WebDriver](https://www.nuget.org/packages/Selenium.WebDriver) C# client:
 using OpenQA.Selenium;

	public class FlaUIDriverOptions : DriverOptions
	{
    public static FlaUIDriverOptions ForApp(string path)
    {
        var options = new FlaUIDriverOptions()
        {
            PlatformName = "windows"
        };
        options.AddAdditionalOption("appium:automationName", "flaui");
        options.AddAdditionalOption("appium:app", path);
        return options;
    }

    public override ICapabilities ToCapabilities()
    {
        return GenerateDesiredCapabilities(true);
    }
	}

	var driver = new RemoteWebDriver(new Uri("http://localhost:4723"), FlaUIDriverOptions.ForApp("C:\\YourApp.exe"))

 Using the [WebdriverIO](https://www.npmjs.com/package/webdriverio) JavaScript client:
 ```import { remote } from 'webdriverio'

const driver = await remote({
    capabilities: {
        platformName: 'windows',
        'appium:automationName': 'flaui'
        'appium:app': 'C:\\YourApp.exe'
    }
});

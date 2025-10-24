# Techniques-for-gaining-an-initial-foothold-within-a-network.
I'll be going over these topics: payloads, droppers, triggers, delivery, containers, and more. 


Payloads:

 -DLL side-loading is great! I will not be going over how to carry out this technique, because there are many indepth articles written on this subject, but I will go over a few key points. 
 
  -DLL hijacking: You can force a legitmate application into loading a malicious DLL. This is not a one size fits all solution though.Finding these vulnerabilities into the Windows OS is not as common as it once was. This is where DLL side-loading comes into play!
  
  -DLL side-loading: The Windows Component Store is located in C:\Windows\WinSxs. The Windows Component Store originally served the purpose of supporting side-by-side assemblies, now it supports several purposes today. WinSxS stores the older versions of dependicies, which reduces conflicts between applications which may require different versions of the same libary. This mean WinSxS may even store vulerably versions of an application even though they've been patched through the main OS. DLL side-loading can come into play in a situation like this. Again, look more into this yourself! I will most likely do a write up on this subject eventually, and I'll most likely include a real life example of this exploit in a video. 

 -AppDomainManager: It is possible to force a DLL being loaded, regardless of the search order. In .NET 3.1 or higher, Startup Hooks can be utilised. Utilize AppDomainManager, either APPDOMAIN_MANAGER_ASM or APPDOMAIN_MANAGER_TYPE. It is also possible to use the appDomainManagerAssembly or appDomainManagerType element in a .config file which must be prefixed with the application you are attempting to load your maliscious dll into, example: ngentask.exe.config  

  -Windows Installer: Visual Studio has an exstention which allows for a Windows Installer to be created. You can add your payload dependincies. 

   -Excel has macros which can be abused. 


   Droppers:

  -Usually, for a payload to be succesfully executed there has to be a dropper. The purpose of the dropper is to evade anti-virus, and to complicate the analysis of the of the infection chain. For right now I will not be going indepth into this subject. 

   Containers:

   -Containers provide a method of bundling the dependencies of your infection chain into a single file (example: trigger, payload, and a decoy). This simplifies the process of sending multiple files, and can add a level of obfuscation, with file password protection. The ISO/IMG, ZIP, AND WIM formats are natively supported by Windows, so one of those file formats can be solid for mnaking a container. There are automatic packing tools, like PackMyPayload or you can pack it manually. Some of these containers support hidden files, and some do not propogate MotW (mark of the web). Mark of the Web is important in this subject matter because it is a zone identifier which marks files that have been downloaded from the Internet as (potentially) potentially unsafe. If you look at a files properties in the Explorer you can see this. This is troublesome because Windows may present additional security warnings to the user before executing your file. Some files, like Office documents will not enable Macros is MotW is present. I highly recommend looking into techniques which can be used to circumnavigate this, like packing a PDF executable into an ISO, and then pulling it from a web server. PackMyPayload has the option to set the hidden attribute on files as they're packaged into a container. This is useful for when you want to hide files such as the decory and payload, so that the user can only see the trigger. A few other methods for getting around MotW: LNK-Stomping, FileFix 2.0. 

   Triggers: 

   -This is the file that the user will interact with after extracting the container. Typically, you want this file to be as easy to activate as possible! 

   -Batch is a text-based file format used for scripting in Windows. The default windows command line interperter, cmd.exe, executes the command lines within the batch file. A batch files may have the .bat, .cmd, or .bmt file type. Typically when a batch file is executed it will print on screen the commands as if they were being typed out. This can be disabled with @echo off, at the top of the batch file. A trick with batch to change its behavior depending on whether the file was double-clicked or executed in command-line. https://x.com/vmray/status/1808903062926315690 

    -Shell Link: a binary file format that is used to create Windows shortcuts. They use a .lnk file exstension, which is not shown in Explorer, regardless if 'show file name exstensions' is enabled. This allows a .lnk file to have filenames like report.pdf.lnk, and the user will only see report.pdf. Lnk files can also be customized with custom icons, so they could link to the cmd.exe but have a PDF icon. One of the easiest way to create a .lnk file is with WScript.Shell COM object via powershell. It's also possible to store and use an ICO file as a dependency inside the container. 

    -Microsoft Saved Console: A technique that Elastic discovered, called 'GrimResource'. GrimResource's uses a specially crafted .msc (Microsoft Saved Console) file and an unpatched XSS flaw to trigger JavaScript code execution, using the Microsoft Management Console. https://gist.github.com/joe-desimone/2b0bbee382c9bdfcac53f2349a379fa4 The weaponised portion of the script is found on line 105. You can URL encode a payload like CyberChef, then paste the encoded string onto line 105. One the MSC file is double clicked it will launch an instance of mmce.exe, which will then spawn cmd.exe. MMC is an auto-elevating binary, so if a user is running as a local admin they will prompted with a UAC prompt, which will turn the payload high-integrity. 

test

# Techniques-for-gaining-an-initial-foothold-within-a-network.
I'll be going over these topics: payloads, droppers, triggers, delivery, containers, and more. 


DLL side-loading is great! I will not be going over how to carry out this technique, because there are many indepth articles written on this subject, but I will go over a few key points. 
  -DLL hijacking: You can force a legitmate application into loading a malicious DLL. This is not a one size fits all solution though.Finding these vulnerabilities into the Windows OS is not as common as it once was. This is where DLL side-loading comes into play!
  -DLL side-loading: The Windows Component Store is located in C:\Windows\WinSxs. The Windows Component Store originally served the purpose of supporting side-by-side assemblies, now it supports several purposes today. WinSxS stores the older versions of dependicies, which reduces conflicts between applications which may require different versions of the same libary. This mean WinSxS may even store vulerably versions of an application even though they've been patched through the main OS. DLL side-loading can come into play in a situation like this. Again, look more into this yourself! I will most likely do a write up on this subject eventually, and I'll most likely include a real life example of this exploit in a video. 

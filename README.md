# Jellyfin UWP Client

WARING : RELEASE 0.8.0 DOESN'T WORK WITH JELLYFIN 10.6 OR HIGHER.


This is a wrapper around Jellyfin's web interface (see https://github.com/jellyfin/jellyfin-web) for UWP devices (Windows 10 & Xbox One)

Steps to install Jellyfin-UWP: 
1. Download and install latest visual studio app from here https://visualstudio.microsoft.com/downloads/
2. Download this repo and extract it.
3. open JellyfinUwp.sln in Visual Studio and left click on Jellyfin (Universal Windows) and go to Publish and click Create App Packages... and select sideloading and then select "Select from the store" and select the name of the certificate (If you created certificate by the step below without changing anything then its name should be JellyfinSigning) 
4. Select an output folder, in architecture select all and in Soulution Configration select "Release ($architecture$)" and click Create. Wait for some time.
5. Open Developer settings and enable "Install apps from any source, including loose files"  
6. Then go to the output folder and open AppPackages, Open Jellyfin_0.8.1.0_Test or any other name of the folder which has Jellyfin in it. Click on Add-AppDevPackage.ps1 and run it with powershell. Wait for some to let it install.

You have installed Jellyfin-UWP and can open it and use it!!

Creating a certificate : https://docs.microsoft.com/en-in/windows/msix/package/create-certificate-package-signing or you need to sign an app package using SignTool which you can find here : https://docs.microsoft.com/en-us/windows/win32/appxpkg/how-to-sign-a-package-using-signtool . 

Steps to create and install an certificate :
1. Open powershell and type:
     
    New-SelfSignedCertificate -Type Custom -Subject "CN=Jellyfin-UWP, O=Jellyfin-UWP, C=IN" -KeyUsage DigitalSignature -FriendlyName "JellyfinSigning" -CertStoreLocation               "Cert:\CurrentUser\My" -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.3", "2.5.29.19={text}")

Change C=IN to your country location like for India type IN, for USA type US. You can change "JellyfinSigning" to anything else but don't change CN and O if don't know what you are doing.
Hit enter.
2. after it is done something like this should appear :

    PSParentPath: Microsoft.PowerShell.Security\Certificate::CurrentUser\My
    Thumbprint                                Subject
    ----------                                -------
    76FE17A65C2B7DCFCA8FC3BA6F292D74890F85D1  CN=Jellyfin-UWP, O=Jellyfin-UWP, C=IN

3. Now press "windows" key and "R" key at the same time and type mmc and hit enter. Press yes.
4. Go to file on the right-top side of the screen and "Add/Remove Snap-in..." and select Certificates from left side of the menu and click add>. Select "My User account" and click finish and click OK. 

5. Click on the Certificates. 
6. Click on Personal.
7. Click on Certificates and left click on Jellyfin-UWP, hover on All Tasks and click Export, click next, on the next window select "No, don't export private key", select "Base-64 encoded X.509 (.CER)", on the next windows type any name you want the certificate to have but don't add any extension in the name, click next and click finish. 
8. Your certificate is stored in "C:\Windows\System32\ $CertificateName$", move it to any other folder, open it and click on "Install Certificate...", select "Local Machine" and click next, Selct "Place all certificates in the following store and click browse and select "Trusted Root Certification Authorities", click next and then click finish. 

or download it from here: https://drive.google.com/file/d/13qLLnqqv3gpFqe_7VKyctCDG4AXqc91a/view?usp=sharing

You have installed your certificate!!

Windows 7 Ultimate/Professional Veewee Definition
=================================================

This uses the All In One "Windows 7 7600 AIO.ISO" from MSDN
file: Windows 7 7600 AIO.ISO
md5sum: ace6c61269613bf515fd59c62185bbcf

I've renamed the file to `win7ult-sp1-x64.iso`

- place it in a directory called iso

The installation uses the Standard way for Windows Unattended installation. The 
XML file was created using the Windows AIK kit, but the file can also be edited by hand.

To edit the Autounattend.xml and validate it:
You can download The Windows® Automated Installation Kit (AIK) for Windows® 7:
url: http://www.microsoft.com/download/en/details.aspx?id=5753
file: KB3AIK_EN.iso
md5sum: 1e73b24a89eceab9d50585b92db5482f

- Building the machine creates a floppy that contains:
  - AutoUnattend.xml (that will configure the windows)
  - winrm-install.bat (activates the http and https listener + punches the firewall hole)

AIK also includes dism, which will allow you to choose a specific version:

If you want to install a different version, edit Autoattended.xml and replace the 
/IMAGE/NAME value with
one of the names listed in the sources/install.wim on the install DVD .iso

```
<InstallFrom>
     <MetaData wcm:action="add">
         <Key>/IMAGE/NAME</Key>
         <Value>Windows 7 ULTIMATE</Value>
     </MetaData>
 </InstallFrom>
```

### Usage - Virtualbox/Vagrant

I'm running these commands on the same machine that I use ChefDK on so my system 
ruby is already set. If you're not, follow the instructions at: 
https://github.com/jedi4ever/veewee/blob/master/doc/installation.md

```
git clone https://github.com/jedi4ever/veewee.git
cd veewee
```

```
gem install bundler
bundle install
```

`git clone atlasrepo here definitions`

`bundle exec veewee vbox build 'win7pro-sp1' 'windows-7sp1-ultimate-amd64'`

Once the Vm is build, enable RDP (Firewall rules are taken care of in the script)
and shutdown with:
`shutdown.exe /s /t 0 /d p:2:4 /c "Vagrant initial reboot"`

`bundle exec veewee vbox export 'win7pro-sp1'`

Add it to vagrant:
`vagrant box add 'win7pro-sp1' 'win7pro-sp1.box'`
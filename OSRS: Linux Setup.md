# Installing OSRS in Linux, 09/2019
## In a Debian VM running on ChromeOS
Extracting launcher from the windows .msi installer, using it run using default-jre. All on bash.

### Get the system upto date
```
sudo apt-get update
sudo apt-get upgrade -y 
```

### Pre-reqs
```
sudo apt-get install -y default-jre p7zip-full

cd ~
mkdir -p tmpOSrs/bak
```

### Download
`wget -O 'tmpOSrs/OldSchool.msi' 'http://www.runescape.com/downloads/oldschool.msi'`

### Extract
```
cd ~/tmpOSrs
cp OldSchool.msi bak/.

7z e OldSchool.msi
cp rslauncher.cab bak/.

7z e -y rslauncher.cab 
mv JagexAppletViewerJarFile.* bak/jagexappletviewer.jar
```

### Setup
```
cd ~
mkdir osrs

cp ~/tmpOSrs/bak/jagexappletviewer.jar ~/osrs/.
```

### Run OSRS in background
* replace <username> with your user name
```
'/usr/bin/java' -Duser.home='/home/<username>/osrs' -Djava.class.path='/home/<username>/osrs/jagexappletviewer.jar' -Dcom.jagex.config='http://oldschool.runescape.com/jav_config.ws' -Dawt.useSystemAAFontSettings='on' -Dswing.aatext='true' -Dhttps.protocols='TLSv1.2' -Dsun.java2d.opengl='false' -Dsun.java2d.uiScale='1' 'jagexappletviewer' 'oldschool' &
```

### Cleanup
`rm -rf ~/tmpOSrs`

### .bashrc shortcut
```
alias osrs="'/usr/bin/java' -Duser.home='/home/<username>/osrs' -Djava.class.path='/home/<username>/osrs/jagexappletviewer.jar' -Dcom.jagex.config='http://oldschool.runescape.com/jav_config.ws' -Dawt.useSystemAAFontSettings='on' -Dswing.aatext='true' -Dhttps.protocols='TLSv1.2' -Dsun.java2d.opengl='false' -Dsun.java2d.uiScale='1' 'jagexappletviewer' 'oldschool' &> /dev/null &"
```

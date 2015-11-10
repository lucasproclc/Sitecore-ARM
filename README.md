# Sitecore on Azure - Azure Resource Manager (ARM) template


## On-premises deployment

<img src="img/legacy.png"></img>

## Azure deployment leveraging SQL Azure

<img src="img/new-saas.png"></img>

## Azure deployment leveraging SQL Server on IaaS

<img src="img/new-iaas.png"></img>





# GIT Deploy




```
echo "Install Git"
powershell -NoProfile -ExecutionPolicy Unrestricted -Command "(New-Object System.Net.WebClient).DownloadFile('https://github.com/git-for-windows/git/releases/download/v2.6.2.windows.1/Git-2.6.2-64-bit.exe', 'Git-2.6.2-64-bit.exe')" && .\Git-2.6.2-64-bit.exe /VERYSILENT /SP- /SUPPRESSMSGBOXES /NORESTART /LOG="git-install.log" 
```


mkdir SARM
cd SARM
"C:\Program Files\Git\bin\git.exe" init
"C:\Program Files\Git\bin\git.exe" remote add -f origin https://github.com/chgeuer/Sitecore-ARM.git
"C:\Program Files\Git\bin\git.exe" remote add origin https://github.com/chgeuer/Sitecore-ARM.git
"C:\Program Files\Git\bin\git.exe" config core.sparseCheckout true
echo ARM/Sitecore-ARM/Templates/ >> .git/info/sparse-checkout
"C:\Program Files\Git\bin\git.exe" pull origin master

git archive --remote=https://github.com/chgeuer/Sitecore-ARM.git master ARM/Sitecore-ARM/Templates/ | tar xvf -


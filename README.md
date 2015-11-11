# Sitecore on Azure - Azure Resource Manager (ARM) template


## On-premises deployment

<img src="img/legacy.png"></img>

## Azure deployment leveraging SQL Azure

<img src="img/new-saas.png"></img>

## Azure deployment leveraging SQL Server on IaaS

<img src="img/new-iaas.png"></img>



# DSC

- Check if one can use https://github.com/iainbrighton/cRemoteFile to download and install GIT locally
- DSC Resource Kit: http://blogs.technet.com/b/heyscriptingguy/archive/2014/10/13/use-powershell-to-download-and-install-dsc-resource-kit.aspx
- [Build Custom Windows PowerShell Desired State Configuration Resources](https://technet.microsoft.com/en-us/library/dn249927.aspx)
- [Writing a Custom DSC Resource](https://www.penflip.com/powershellorg/the-dsc-book/blob/master/writing-a-custom-dsc-resource.txt)
- [Using PowerShell Desired State Configuration to check for and install applications](https://justingalston.wordpress.com/2014/06/11/using-powershell-desired-state-configuration-to-check-for-and-install-applications/)

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

# Requests

## Initial request

Sets the `ARRAffinity` cookie

```
GET http://104.40.211.199/ HTTP/1.1
Host: 104.40.211.199

HTTP/1.1 200 OK
Set-Cookie: ARRAffinity=6f6eb54d3b6d7ed13173b9203b0bd6571b611d626818fba77a815805a7c90146;Path=/;Domain=104.40.211.199

Hello, web-0
```

## Client pinned to instance web-0

```
GET http://104.40.211.199/ HTTP/1.1
Host: 104.40.211.199
Cookie: ARRAffinity=6f6eb54d3b6d7ed13173b9203b0bd6571b611d626818fba77a815805a7c90146

HTTP/1.1 200 OK

web-0
```

## Client pinned to instance web-1

```
GET http://104.40.211.199/ HTTP/1.1
Host: 104.40.211.199
Cookie: ARRAffinity=0d2b622183005143ec3cc16114675396cc39baeb1d91bb28025c585c12279a00

HTTP/1.1 200 OK

Hello, web-1
```


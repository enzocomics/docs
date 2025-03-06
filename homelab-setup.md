## **Install Speedtest**
(Because I wanted to know if my 2.5gb ethernet card was working)
- `curl` doesn't work directly from github for some reason, so download the file locally: https://github.com/taganaka/SpeedTest/archive/refs/heads/master.zip
- From the local folder, copy the zip to the server `scp SpeedTest-master.zip root@server:/root/.`
- Install dependencies: `apt install zip build-essential libcurl4-openssl-dev libxml2-dev libssl-dev cmake`
- Open the archive: `unzip SpeedTest-master.zip`
- Navigate to the folder `cd SpeedTest-master` and then run `cmake -DCMAKE_BUILD_TYPE=Release .` and `make install`

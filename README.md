# PoGoMap
The fastest pk Go map available.

Heavily using [pgoapi](https://github.com/keyphact/pgoapi). Shout-out to the Unknown6 team!

![image](https://cloud.githubusercontent.com/assets/1723176/17482369/bf3df2b2-5d81-11e6-904e-edfd496702dc.png)

##Installation:

**Note:** If you are upgrading from the last version, you will have to update and/or reinstall the requirements.

1. Clone the repository `git clone https://github.com/favll/pogom.git`
2. Install the dependencies `pip install -r requirements.txt`
3. Start the server by running `python runserver.py`

**Pro-Tip:** Use the `-H` and `-P` flag to specify host and port. E.g. `-H "127.0.0.1" -P 5001` will tell the webserver to listen to localhost requests on port 5001. You can then head over and take a look at the map at `http://127.0.0.1:5001/`. If you want the server to listen on all public IPs use the host `0.0.0.0`. This will allow you to access your server from other machines.

There's no other flags besides  `-H` and `-P`, everything else is configured through the Web UI.

##Usage

 - Visit `http://<ip>:<port>/` (by default: `http://127.0.0.1:5000/`)
 - On the first run you will be redirected to a configuration page
   - Enter your Google Maps Api Key
   - Enter all accounts and passwords to be used for scanning
   - Optionally protect the configuration with a password (only authenticated users can access the config and change scan locations)
 - Go back to `http://<ip>:<port>/` to view the map
 - Add scan locations simply by clicking on the map

##Features
- [x] Extremely fast (using multiple accounts)
- [x] Multiple locations
- [x] Perfect coverage (using a perfect hexagonal grid of radius 70m)
- [x] Everything configurable from the browser (bye bye command-line flags)
- [x] Hide common pk
- [x] Server status in the Web-GUI
- [x] Stats about seen pk
- [x] Mobile friendly

##TODO
- **Notifications**
- Show/Hide Pokestops
- Heatmaps!

##FAQ

**The scan is too slow!**

Due to Niantic's throttling we can only do one scan every 10 seconds from each account. Each scan only gives us the pk in a 70 meter radius around the center. This means, to scan a radius of one kilometer, we actually need to scan about 250 individual locations. If you are using only five accounts, this will take about 500 seconds (`250/5*10s = 500s`). With 100 accounts it will be finished in 25 seconds. So the solution is to add more accounts.

**How many accounts should I use?**

More = Better. But at about 200 accounts you will get diminishing returns because you're bottlenecked by other things (networking, parsing responses, DB). This is of course dependent on your system's performance, so your mileage may vary.

**It should scan multiple locations in parallel!**

The tool does scan all locations, but successively. Your actual problem is that you either have too few accounts or a too large area (see the calculation in the first question). Even if we change the order, the total runtime would stay the same. 

**I'm getting errors such as `Server seems to be busy or offline!`, `Unexpected error during request: ...`, `Received empty map_object response. Logging out and retrying.`, `Request throttled by server... slow down man`**

A certain number of failing requests is to be expected, as the Niantic servers are still somewhat unstable. The program handles the errors gracefully and tries again for a few times until it succeeds. It prints the error messages for debugging purposes. Unless it is a fatal crash and not all the requests fail, everything is fine. Also check if the servers are maybe completely unavailable for you, before opening an issue. 

**I'm getting the error `Seems your IP Address is banned or something else went badly wrong`**

Niantic blocked the IPs of several popular cloud providers such as Amazon, Digital Ocean, Google, etc. Try it on a different server.



[![Deploy on Scalingo](https://cdn.scalingo.com/deploy/button.svg)](https://my.scalingo.com/deploy?source=https://github.com/waiyin21/test123)


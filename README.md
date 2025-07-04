# Tesla STEM High School EESD Raspberry Pi Smart Garden

This repository includes all the **code** you need to get started with the Tesla STEM Smart Garden (or even one of your own)!

If you are curious about this project, Don't be afraid to email [@somebody4545](https://github.com/somebody4545) on GitHub for access to more documentation.

If you are doing this for an EESD project, contact me via a school email on my school email, or when I graduate, contact me with your **personal** email. 

# Prerequisites
- Raspberry Pi
    - 3b+ *works*, there are no CAD files for a case for it
    - 4 has a case created for it

- Assembled system (additional info in our CAD files in the Legacy Project folder)
    - Grove Base Hat for Raspberry Pi
    - One Wire moisture sensor (PIN `D5`)
    - DHT11 (Humidity + Temp) (PIN `D16`)
    - SI1151 (Sunlight) (PIN `I2C`)
    - Relay (PIN `D18`)
    - 4 Analog Moisture Sensors (PINS `A0`, `A2`, `A4`, `A6`)

- A domain (unless sticking to fully local)
    - With the domain, it is preferable to use Cloudflare Tunnel as the passthrough solution

# Run the Project

## Step 1: Set up the RPi
- **YOU WILL NEED A WAY TO REMOTELY ACCESS THE SYSTEM!!!!**
    - Figure this out **FIRST**, if you don't have an easy way to do this, you will be finding yourself having to run back and forth a lot. 
    - This can be done with Raspberry Pi Connect (recommended), but if you're a bit more technical and feel like it, SSH is also a fine solution.
    - The current system's implementation of this can be found in the less publicly accessible Legacy Projects folder

- Install the Raspberry Pi into the system with the Grove Base Hat, and match the GPIO pins mentioned
- Go to Preferences > Raspberry Pi Configuration > Interfaces and ensure the following are on, then restart
    - Remote GPIO
    - 1-wire
    - I2C

## Step 2: Prepare to run
> This is the fun part where version changes and other issues can completely ruin it all. If you would like a working venv to work with, the current garden has it already, but I sincerely hope this works and we can all go about our day happy. I am open to help out with this section. It may take longer than you think. Blame Seeed.

### Installing libraries
- I created bash scripts to make your job a little easier. Here's a simple one liner that should work if you (and I) did everything right:

    ```bash
    git clone https://github.com/MrChuhal/Smart-Garden-Arduino.git && cd Smart-Garden-Arduino && chmod +x *.sh && ./setupPython.sh && ./setupSite.sh
    ```
- I recommend digging in to know what you're actually doing, but this should work just fine.
  
### Bash Script Summary
- `setupPython.sh`: Sets up a Python virtual environment and installs required libraries.
- `setupSite.sh`: Installs NVM and sets up the frontend environment.
- `run.sh`: Starts both backend and frontend servers.

- **Restart** once it is all completed

### Refactor
- This code assumes your Raspberry Pi user's home directory is `/home/inesh/`, which I doubt. You should be able to Ctrl+Shift+F and click open the menu to find and replace each occurence of this with the appropriate directory. If someone can create a PR to handle this in an easy way, I'd be more than happy to merge it. 

## Step 3: Run it!
### Cloudflare Tunnel
- If you have a domain, this is where you'll have some more set up.
- Here, I'd recommend you do some research on Cloudflare Zero Trust to create a tunnel, and likely on a school network, you'll need to use Cloudflare Warp on top of it (instructions for these are online, and likely more accurate)
- Ensure the port the site points to is `localhost:3000`
> [This guide](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/install-and-setup/tunnel-guide/) is what you're looking for to create the tunnel
### Run script
After the previous set up, installing should be as easy as:

```bash
./run.sh
```
You can run this project fully offline on localhost:3000 if you skip the Cloudflare Tunnel setup.
You should now be able to check out the site at `http://localhost:3000`, or whatever your tunnel URL is!!! Give yourself a pat on the back.

## To-Do
- [ ] Live camera stream display on dashboard
- [ ] CSV export download button
- [ ] Editable pump thresholds in UI


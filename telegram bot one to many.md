



#driver #chromedriver #working #link


#run the #bot within #environment in #wsl1 on #vps

Below is the **cleanest, repeatable sequence** to get the bot running from `/opt/bot/bots`.  
Copy-&-paste the block **one line at a time** (don’t skip the `source …` step).

```bash
# 0) (Already) cd /opt/bot/bots
pwd                         # should print /opt/bot/bots

# 1) Create / activate a Python-3.8 virtual environment
python3.8 -m venv venv      # creates ./venv  (run once)
source venv/bin/activate    # puts you into the venv; prompt shows “(venv) ”

# 2) Make sure this venv’s pip is up to date
pip install --upgrade pip setuptools wheel

# 3) Install the exact libraries your code expects
#    • python-telegram-bot ≥20 (has Application/CallbackContext, etc.)
#    • selenium 4 (with the ‘service=Service(…)’ constructor)
pip install "python-telegram-bot>=20,<21" \
            "selenium>=4.27,<4.28"

# 4) Quick sanity-check – should print versions, no traceback
python - <<'PY'
import sys, selenium, telegram
print("Python               :", sys.version.split()[0])
print("python-telegram-bot  :", telegram.__version__)
print("selenium             :", selenium.__version__)
PY

# 5) Make sure Chrome & chromedriver can be found
#    (adjust the paths if you installed them elsewhere)
export CHROME_BIN=/usr/bin/google-chrome
export PATH=$PATH:/opt/bot/chromedriver           # folder that contains ‘chromedriver’

# 6) Run the bot
python bot.py
```

_While you stay in the same shell the venv remains active; if you open a new  
terminal just `cd /opt/bot/bots && source venv/bin/activate` and continue._

---

### If you need the bot to keep running after you log out

```bash
# still inside the venv, still in /opt/bot/bots
sudo apt-get install -y screen      # (tmux works too)

screen -S telegram-bot              # opens a new screen session
python bot.py                       # start the bot
# Press  Ctrl-A  then  D  to detach
# Re-attach later with
screen -r telegram-bot
```

That’s the whole setup: create venv → install libs → export paths → run.
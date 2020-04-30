# Configuring the ATM

## 💻 Access the ATMs configuration file

There is a configuration file that lets us make changes to the core configurations of the ATM such as the currency displayed and more.

The configuration file will be created, the first time the ATM is turned on an run with `./app.py`. Make sure you've run `./app.py` at least once, otherwise this configuration file won't exist.

The configuration file can be found here: `~/.lightningATM/config.ini`

Let's inspect 🔎 what is inside this file with the editor `nano`. Type in the following to open the file with the `nano` editor:

```text
nano ~/.lightningATM/config.ini
```

The beginning of this configuration file will look something like this and we'll quickly check the most important values in there:

```text
[atm]
# Set your fiat currency with the three letter
# currency code (https://www.xe.com/symbols.php)
cur = eur

# Define what a cent is called in the currency
# of your choice for price display (singular).
centname = cent

# Set the Fee in %
fee = 2
```

* `cur = eur`

  The variable `cur` defines what fiat currency will be used at your ATM.

* `centname = cent`

  The variable `centname` defines the name of one cent of your base currency \(0.01\)

* `fee = 2`

  The variable `fee` defines how much fee you charge those who use your ATM

You can now move with your cursor to the desired variable and simply change it to your liking. I'd recommend to only change those three values and leave the rest as it is \(unless you know exactly what you are doing 👆 \).

In order to save the file and exit you will have to press `Ctrl + x` and it will ask you `Save modified buffer?`. You can confirm by entering `y` \(for yes\) and hitting `Enter` to confirm.

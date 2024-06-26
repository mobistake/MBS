![Example-Logo](https://sappcoin.com/wp-content/uploads/2021/05/Mobistake-logo-transparent.png)

# Mobistake Masternode Setup Guide
***
## Required
1) **MBS collateral value at current block** ([consult the collateral table](../../README.md#rewards-breakdown))
2) **Local Wallet https://github.com/mobistake/MBS/releases/latest**
3) **VPS with UBUNTU 20.04** (it is possible to work on other versions but it is not tested)
4) **Putty https://www.putty.org/**
5) **Text editor on your local pc to save data for copy/paste**
***

***On your Local Wallet***
* Create an address with a label MN1 and send exactly the collateral amount to it ([consult the collateral table](../../README.md#rewards-breakdown)).
 Wait to complete 6 confirmations on “ Payment to yourself “ created.
 Or 15 confirmations if sent from an external wallet.

* Open the Debug Console ( Tools – Debug Console ) and type ***createmasternodekey***.
You will then receive your private key, save it in a txt to use it later.
  ```
  Example:
          createmasternodekey
          8mTdWPF8Pbc6aTS36W5koLYZWSo5Jby5UJZWCAjDMo7AJYbBwy5
* Still at Debug Console type ***getmasternodeoutputs*** and save txhash and outputidx on a txt
  ```
  Exemple:
          "txhash" : "726f3c137b1c567efdbe3bf0b0a061437a8ed52e515e709868d0623b73a31aee",
		         "outputidx" : 0

***On Putty***

* Once logged in your vps, *copy/paste* each line one by one with *Enter*

```
wget -q https://raw.githubusercontent.com/Mobistake/Mobistake/master/contrib/masternodesetup/masternodesetup.sh
```

```
chmod +x masternodesetup.sh && bash masternodesetup.sh
```

* Let this run, and when it ask you to install dependencies, if you're not sure press ***y*** and then enter

* It will take some time and then will ask to compile the Daemon, press ***y*** and then enter 

* Last thing script will ask you is to provide Masternode Genkey. Copy the one you got previously (createmasternodekey) and press enter.

Remember to do `mbs-cli getblockcount` to check if VPS catching blocks till it synced with chain, if not follow this procedure:

* Go to your wallet-qt and check peers list (tools - peers list) and select one ip from the list. With that ip do the follow command at VPS `mbs-cli addnode "ip" onetry`

      Example:
		  mbs-cli addnode seed01.mobistake.app onetry
		  mbs-cli addnode seed02.mobistake.app onetry
		  mbs-cli addnode seed03.mobistake.app onetry
		  mbs-cli addnode seed04.mobistake.app onetry
		  mbs-cli addnode seed05.mobistake.app onetry
		  mbs-cli addnode seed06.mobistake.app onetry
		  mbs-cli addnode seed07.mobistake.app onetry
		  mbs-cli addnode seed08.mobistake.app onetry
		  mbs-cli addnode seed09.mobistake.app onetry
		  mbs-cli addnode seed10.mobistake.app onetry

    
* Check now if VPS already downloading blocks with the command `mbs-cli getblockcount`, and if yes give it time now to catch last block number 

Do not close your terminal/ command prompt window at this point.

***Go back to your Local Wallet***

* Open the Masternode Configuration file (tools – open masternode configuration file) and add a new line (without #) using this template (bold needs to be changed) in the final save it and close the editor

**ALIAS VPS_IP**:4855 **masternodeprivkey TXhash Output**

		Example:
		MN1 149.28.232.213:4855 8mTdWPF8Pbc6aTS36W5koLYZWSo5Jby5UJZWCAjDMo7AJYbBwy5 726f3c137b1c567efdbe3bf0b0a061437a8ed52e515e709868d0623b73a31aee 0

* Close and Re-open Local Wallet, and at Masternode Tab you will find your MN with status MISSING

***(For the next steps you need to have already 16 confirmation on “Payment to yourself “ created in first step)***

* Go to Debug Console type the following: ***startmasternode alias 0 (mymnalias)***

		Example:
		startmasternode alias 0 MN1
***

***Go back to Putty***

```
mbs-cli getmasternodestatus
```

You need to get **"status" : 4** 

## Congratulations your Mobistake node is running

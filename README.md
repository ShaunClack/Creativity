# Creativity

Earn Crypto Mining with Free credit:)

You are reading the detailed instructions for mining Cryptonight-coins (basic mining-knowledge is assumed). 
The rate can fluctuate between 1:1 and 1:10, i.e. in the best case you'll get almost 1$ worth of cryptocurrency for every 1$ spent on azure (depending on the current exchange-rates). With an MSDN Enterprise subscription you can mine cryptocurrency worth up to 149$ every month! This is possible because the newly introduced Azure-batch-service has a low-priority-option, which is dirt cheap!
Short summary:

    You'll need a azure-account with free-credit, e.g. from a MSDN-subscription
    Chose a mining-pool and setup a wallet
    Start mining with the Azure-Batch-Service using the scripts provided here

Setup Azure with Free Credit

Do you have a MSDN-subscription from your day job? Great! You must have already noticed that Microsoft keeps sending you emails asking you to open an azure-account with up to 150$ monthly credit. Follow the instructions in the mail to claim your free credits. Note that by default you don't even have to enter your credit-card-number, so you can be sure that your mining is running purely on your monthly free credit.

Even if your company pays for the MSDN-subscription, the associated azure-account is your personal account and completely separated from the company. Your boss has no way of accessing it. Microsoft encourages people to use the free credits for testing and learning, and this is what you'll do: learning about using the azure-cloud and the blockchain-technology in a very practical way :-)

Note: It is your responsibility to comply with Azure's ToS. You will be banned very quickly if you do something that Azure does not like. You should only use free credits from legitimate sources (e.g. if you have a MSDN-subscription from your day-job).
Chose Mining-Pool

The scripts provided on this site support mining with all algorithms supported by xmr-stak. Besides Monero (XMR) these are BBSCoin (BBS), BitTube (TUBE), Free Haven/Swap, Graft (GRFT), Haven (XHV), Intense/Lethean (LTHN), Masari (MSR), Quantum Resistant Ledger (QRL), RYO and TurtleCoin (TRTL). Other coins might also work if they are based on a cryptonight-algorithm (you can use cryptunit to calculate your expected profits).
To start mining you'll need to choose a mining pool. There should be a list of available mining-pools somewhere on the homepage of your desired coin (e.g here's a list of Monero-pools). Pay attention to the pool's rules:

    What are the pool's fees? This just means that your payout is decreased by the given percentage.
    What is the pool's minimum payout? Depending on your hashrate it might take a month or longer until you reach the limit and you get the coins in your wallet.
    Reward method PPS or PPLNS? With PPLNS the miners get their share only once the pool finds a block, so for small pools it might take several days until you can see a non-zero pending balance for your wallet on the pool's website.

You'll also need to setup a wallet:

    For Monero probably the easiest way to get started is using a webwallet from mymonero.com (take care that you don't fall victim to a phishing site: always check your browser's address bar before entering your password!).
    For coins other than Monero read the coin's homepage for information on how to create a wallet.

You have the option to setup a secondary pool, so that your VM's can keep working even if your primary pool is offline (it has to be the same cryptocurrency, though).

Note: Cryptocurrencies are notorious for being targets of spectacular hacks and scams. The more cryptocurrency you accumulate, the more important it is to educate yourself about the possible security threats!
Setup the Azure Batch-Service

Note: Azure calls a group of virtual machines within the batch-service a 'Pool'. This has nothing to do with the term 'mining-pool' (operated by e.g. supportXMR.com). Don't confuse the two terms.

After signing up for your azure-account you can click on the following link to create a new batch-account: https://portal.azure.com/#create/Microsoft.BatchAccount. I recommend using Chrome to access the azure-portal. Fill the form with the following information:

    Resource Group: Click 'Create New' and give it a name, e.g. 'myRecGroup'
    Account name: Just a name for your batch-account
    Location: Choose 'East US'
    Leave the other options at the default-settings.
    Click on 'Review+Create' at the bottom and then on 'Create' on the following page to create the batch-account

Once you get the notification that your batch-account has been created (it will take a few seconds), go to your batch-account (link to your batch-accounts: https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Batch%2FbatchAccounts) and create a new pool: select 'Pools' and then click 'Add'. Fill the form with the following information:

        Section 'Pool Detail':
        Pool ID: Just a name for your azure-pool
        VM Size: 'Standard F2 (2Cores, 4GB)'
        (Choose the exact type! Otherwise you will not get the optimal hashrate!)
        Section 'Operating System':
        Publisher: Canonical
        SKU: 16-04 LTS
        Leave the other options at the default-settings.
        Click on 'OK' at the bottom to create the azure-pool.

In order to make the nodes actually do something, you'll need a startup script which downloads the mining-executable and starts mining. You can create your personalized script here by filling out the fields:

    Currency to mine:
        If you choose a specific coin, the algorithm will be automatically updated if the coin changes its algorithm. If your coin is listed this is typically the best option.
        If your coin is not listed, choose the suitable generic algorithm. However, if your coin changes its algorithm you'll have to update your startup-script yourself.
        If you mine at a pool with auto-selection of coins like MoneroOcean.stream choose the suitable generic algorithm.

    Primary mining-pool.
        Wallet for primary mining-pool:
            Your personal wallet. A random string of characters similar to: 4999aeniCU9Ug67vs7yvyJTSkxVUZRirUYUerT66fqzoYMhiShFLBqZHmFxmPD6oABafM5cVKc77yj3Fypvi9CDRTYEvDPL
             

        Address of primary mining-pool:
            some examples of pool-addresses (i am not affiliated with any of the pools. I have personally used them, though):
            Pool-Address 	Pool-Name 	Payout-Currency 	Required Currency-Setting
            pool.supportxmr.com:5555 	supportXMR.com
            (Monero-pool)
            	XMR 	Monero (CryptonightV8)
            gulf.moneroocean.stream:10001 	MoneroOcean
            (pool with auto-selection of CN_R-coins) 	XMR 	Generic Cryptonight_R
            pool.XXX.hashvault.pro:80
            (Where XXX can be Graft, Haven, ...)
            	hashvault.pro
            (Follow link to see the supported currencies.) 	different cryptonote-coins 	Graft, Haven, ...

        Password for primary mining-pool:
            Read your pool's documentation to find out how to use this field. In most cases you can just leave it at 'x'
    Secondary mining-pool. This pool will only be used if the primary mining-pool is offline. Leave the fields empty if you don't want to use a secondary mining-pool.
        Wallet for secondary mining-pool:
             
        Address of secondary mining-pool:
             
        Password for secondary mining-pool:
             


This is your personalized script:

Once the azure-pool is created, go to 'Start task'. Fill the form with the following information:

    Command line: here you have to copy&paste your personalized script from the textfield above
    User identity: 'Task Autouser, Admin'
    Leave the other options at the default.
    Click on 'Save'

The last step is to tell Azure how many mining-nodes it should start for you. This depends on the amount of free credits available in your azure-account. Basically you want to use up as much of your monthly credit as possible without actually consuming all of your credit (otherwise you'll have to repeat the setup again in the next month because azure will delete your pools if your free credits are exhausted).

	Professional 	Platform 	Enterprise
Number of low priority nodes (F2, 2 Cores, 4GB) 	3
	6
	9
Total number of active cores 	6 	12 	18
Cost of nodes for 31 days 	~48$ 	~97$ 	~145$
Monthly free credit 	50$ 	100$ 	150$

If azure is using your local currency instead of USD the numbers might look slightly different. If you run out of free credit before the end of the month, just reduce the number of nodes by one and try again. 

Now go back to 'Overview' and click on 'Scale'. Enter the number from the table above in the field 'Low priority nodes' (e.g. 3 if you have MSDN Professional), and click on 'Save'. Congratulations! The azure cloud is now mining cryptocurrency for you!
To stop your azure-pool, go to the overview-page of the azure-pool, select 'Scale' and enter '0' as the number of 'Low priority nodes'. Then click 'Save'. Note that by default your azure-pool will automatically stop when your free credits are exhausted. You can simply restart your azure-pool in the next month once your free credits have been refilled.
Watching your Mining-Progress
The following information only applies if you are mining Monero at supportXMR.com. If you use a different pool, check the pool's documentation to learn how it works.
If your are using supportXMR.com you can see your mining-status if you go to the pool's dashboard supportXMR.com/#/dashboard (or click on the "Dashboard"-link on the left pane of the pool's homepage), scroll down to the bottom of the page and enter your wallet.

    The VM takes around 5 minutes to startup and compile the mining-software. After that you will see the number of submitted hashes slowly increasing. The displayed hashrate will vary wildly - this is normal.
    Your pending balance will increase once the mining-pool finds a new block and it reaches the maturity depth. For a big pool like supportXMR.com this will take an hour or so. However, if the pool is smaller or unlucky, it can also take a lot longer.
    The pending balance will be paid out to your wallet once it passes the minimum payout threshold. The default threshold of supportXMR.com is 0.3 XMR.
    If you want to login to supportXMR.com in order to change the minimum payout threshold, you can first run your VMs with the startup-script generated by the quickstart-instructions (it will set the default-password 'azurecloudminingscript'). After you have submitted a share the login will be created and you can change the password through the GUI at supportXMR.com. The login is linked to the wallet, once it is created you can change the startup-script back to what you originally wanted. 

Important Notes:

    Some reasons why the hashrate displayed by the pool will vary a lot:
        Azure is running many virtual machines on a single physical server. If you are lucky the other virtual machines are running idle and you'll get a higher hashrate. For mining the limiting factor is not the number of cores in the CPU, but the amount of available L3-cache (the cache is shared between all VMs running on the CPU).
        In exchange for the low price azure does not guarantee 100% availability for the low-priority-VMs (in my experience the VMs are in fact available most of the time, though).
        The hashrate displayed by the pool is calculated from the number of submitted shares (i.e. shares which exceed the custom difficulty of the pool), not from the number of hashes your miner has actually calculated.
    Options for optimizing your hashrate
        In my experience azure-pools with fewer nodes result in the highest hashrate. So instead of setting up one azure-pool with e.g. 10 nodes you can setup 5 pools with only 2 nodes (you can use the identical startup-script for all azure-pools). This is because azure tends to allocate all nodes of a pool on a single physical CPU.
        You can also experiment with setting up your azure-pools in different regions. However, note that only few regions are actually available for use with free credits (East US, Southeast Asia and a few more) and that other regions may be more expensive than East US (if necessary, you'll have to reduce the total number of nodes to stay within your monthly free credits)
        All in all you can expect around 70H/s per used core when mining Monero and around 55H/s per used core when mining CN-Heavy.
    Many pools support assigning a worker-ID to your miners. The pools typically display the achieved hash-rate for each worker-ID separately. Read the pool's documentation to find out how it works exactly. Some pools expect the ID as a suffix to the wallet, then you can just enter it in the form before generating your startup-script. Other pools (like supportXMR) expect the ID in the password-field. In that case you can edit the generated startup-script by hand. Additionally, there are some variables which you can use as well (compare it to the startup script generated by the quickstart-instructions to see how it should look like):
        ${AZ_BATCH_POOL_ID}    : The name of the azure-pool used
        ${AZ_BATCH_ACCOUNT_NAME}    : The name of the azure-batch-account used
        ${AZ_BATCH_NODE_ID}   : The name of the azure-pool-node. Typically this is a complicated name with some special characters. Use at your own risk!
    Azure has a standard-limit of 20 low-priority-cores per region. If the quota in your azure-account is less than that, you can request an increase of this quota through the azure support. I recommend not asking for more than 20 cores. We are operating in some kind of gray area here, you don't want to cause a big stir... If you want to mine with more than 20 cores i recommend setting up more azure-pools in other regions (the quota limits only the number of cores per region, nothings stops you from setting up more azure-pools in other regions).
    The script will restart itself every 2 days, fetching the latest version of the miner-executable from github. This is required because the mining-algorithm is regularly modified in order to prevent the development of ASIC-miners for Monero. If you don't like this behaviour you can change the phrase './run_xmr_stak.pl 30;' to './run_xmr_stak.pl;' in the generated script (i.e. remove the '30'). However, note that then you will have to manually restart your mining-pools in order to get the updated miner-software.
    Nothing in life is free. If you are mining with the script from this site the miner-executable will mine 4% of the time to my private wallet. From the cryptocurrency generated this way i pledge to donate half (2%) to the authors of xmr-stak. You can view this as a convenience-fee for getting a tested and streamlined mining-script.

Do you need help following the instructions? You can contact me at shaunclack9@gmail.com


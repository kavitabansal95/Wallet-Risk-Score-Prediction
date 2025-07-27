# Wallet-Risk-Score-Prediction

### **Assignment: Wallet Risk Scoring From Scratch**

### **Instructions:**

### Given your experience working with the aave V2 protocol, it's assumed that you have a clear understanding of lending protocols and on-chain transaction analysis.

In this assignment, you are provided with a list of wallet addresses. Your task is as follows:

1. **Fetch Transaction History:**
    - Retrieve the transaction data for each provided wallet address from compound V2 or V3 protocol.
2. **Data Preparation:**
    - Organize and preprocess the transaction data to create meaningful features that can reflect each wallet's risk profile.
3. **Risk Scoring:**
    - Develop a scoring model that assigns each wallet a risk score ranging from **0 to 1000**.
    - Clearly document your feature selection, normalization method, and scoring logic.
  
      - A brief explanation detailing your:
      1. **Data Collection method** : Used covalenthq to fetch transaction history of wallets 
      2. **Data cleaning & feature engineering** :
          a.) Redudent features removal eg (from_address_label','to_address_label' ,'miner_address'...)
          b.) null or blank value treatment
          c.) Feature extraction and dropped redudent features.
          d.) Again null & infi value treatment after new features extraction
          e.) correlation matrix visulaization and correlated feature removal
          f.) data scaling
     3. **Scoring method**
          a.) K-means clustering to identify nature of data(k=6 identified)
          b.) cluster visualization and scaling
          c.) Weight disctribution of features and scaled the risk score for values to be between (0-1000)
     4. **Justification of the risk indicators**:
          a.) tx_count (Weight: 0.15): High transaction counts (e.g., Wallet 0: 2404) indicate potential bot or laundering activity, while low counts (e.g., Wallet 2: 4) suggest low risk.         Critical for detecting active wallets in AML frameworks.
        
          b.) failure_count (Weight: 0.12): More failed transactions (e.g., Wallet 0: 50) signal errors or malicious attempts, increasing risk. Low failures (e.g., Wallet 1: 0) indicate                                                      stability.
        
          c.) unique_from_addresses (Weight: 0.15): Many unique senders (e.g., Wallet 0: 365) suggest mixing or scams, a key AML indicator. Few senders (e.g., Wallet 1: 3) imply low risk.
        
          d.) avg_tx_value_eth (Weight: 0.12): High transaction values (e.g., Wallet 0: 4.22e+18) may indicate fraud or whale activity. Low values (e.g., Wallet 2: 4.65e+15) are less risky.
        
          e.) avg_gas_spent (Weight: 0.08): High gas usage (e.g., Wallet 3: 1.65e+06) reflects complex transactions, potentially risky. Low usage (e.g., Wallet 1: 6.17e+04) suggests simplicity.
        
          f.) avg_fees_paid (Weight: 0.06): High fees (e.g., Wallet 3: 2.16e+16) may indicate urgency or spam, less critical than gas spent.
        
          g.) gas_price_avg (Weight: 0.05): Higher gas prices (e.g., Wallet 2: 5.85e+10) suggest prioritized transactions, a minor risk indicator.
        
          h.) gas_quote_avg (Weight: 0.04): High gas quotes (e.g., Wallet 3: 41.18) reflect costly transactions, with minimal risk relevance.
        
          i.) contract_creation_sum (Weight: 0.10): More contract creations (e.g., Wallet 0: 11) can signal scams or DeFi risks. None (e.g., Wallet 1: 0) is safer.
        
          j.) wallet_age_days (Weight: 0.08): Newer wallets (e.g., Wallet 1: 0) are riskier; older ones (e.g., Wallet 0: 2972) may be stable, though not always.
        
          k.) success_rate (Weight: 0.10): Lower success rates (e.g., Wallet 0: 0.979) indicate errors or fraud; high rates (e.g., Wallet 1: 1.0) suggest reliability.
        
          l.) in_out_ratio (Weight: 0.10): Extreme ratios (e.g., Wallet 0: 3.15, Wallet 3: 0.36) may signal laundering or scams, unlike balanced ratios (e.g., Wallet 2: 1.0).
          m.) avg_tx_per_day (Weight: 0.05): High frequency (e.g., Wallet 0: 0.809) suggests risky activity; low frequency (e.g., Wallet 2: 0.0) indicates stability.
          
           Summary: These indicators are justified by their alignment with blockchain risk patterns (e.g., high activity, failures, or complex transactions signal higher risk). Weights reflect                        their relative importance, with tx_count, unique_from_addresses, and failure_count being most critical for detecting suspicious behavior in cryptocurrency wallets.

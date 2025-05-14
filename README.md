# ML Final Project

Final Project for CS-424: Intro to Machine Learning

Group: Jess M., Anthony L., Anthony W.

# Overview of the Project
**Problem:** 
We wanted to train a model to analyze a cybersecurity dataset with the goal of detecting various malicious attacks. We achieved this by creating 2 models, a “Defender” model that classifies the data based on specific parameters into either a benign action or an XSS, Brute Force, or SQL Injection attack, and an “Attacker” model that generates different types of attacks within a specific data range, with the ability to mimic either harmful or malicious events.

**Data:** 
Our dataset was pulled from  [CIC-IDS-2017](https://www.unb.ca/cic/datasets/ids-2017.html), and is a cleaned dataset from the University of New Brunswick, intended to provide a realistic, labeled dataset of network traffic for machine learning-based security research. We focused on the Thursday Working Hours Morning WebAttacks file which has 79 numerical features, as extracted by the CICFlowMeter tool from network packets. These features are primarily statistical measures of network flow characteristics, designed to capture patterns related to the various web attack types. Each network flow is labeled with a category: BENIGN (normal traffic) or one of the attack types (Web Attack  XSS, Web Attack  SQL Injection, Web Attack  Brute Force). The dataset has heavy class imbalance, with far more benign traffic than attack traffic and the attack types themselves are imbalanced as well.

**Model:** 
We created 2 models to solve our problem, with both of them being able to feed off of each other. The first one is our defender model, which is a multi-class classification model designed to identify different types of web attacks (Brute Force, SQL Injection, XSS) while also recognizing benign traffic. The goal is to maximize correct classifications across all classes while minimizing misclassifications between attack types. This model implements data preprocessing to ensure data quality and compatibility, feature scaling to normalize feature ranges, SMOTE (synthetic Minority Over-sampling Technique) to try and address the imbalance in classes we have in our data, and implements XGBoost as the classification algorithm. This specific algorithm was chosen due to its ability to handle complex, non-linear relationships in network traffic, its built-in handling of imbalanced data and its strong performance when dealing with tabular data. The main design decisions we made were splitting the data before preprocessing to prevent data leakage, scaling the data before implementing SMOTE so that it isn’t affected by different feature scales, and implementing SMOTE instead of undersampling our benign samples to reflect the data more accurately.

**Results:**
If we had more time and more sophisticated technology, we would have liked to do the following in order to train the model better. For the defender model specifically, feature engineering could be a huge improvement in order to better differentiate the attacks. Our model has trouble distinguishing between Brute Force and XSS, so this could help address our issue. If given access to more GPU overhead in Colab, we could implement Hyperparameter tuning in order to optimize parameters in each of the models, and run the adversarial loop for more iterations and make it more sophisticated. As for the attacker model, we could use a more stable GAN variant (like WGAN-GP) and a stronger, differentiable surrogate that better mimics the XGBoost boundary, which could yield to smoother training and more realistic flows. Additionally, adding a conditional GAN structure would let us tailor adversarial samples to each attack type, and enforcing protocol constraints (e.g. valid port ranges or integer packet counts) would keep generated traffic plausible. Lastly, incorporating some diversity to promote losses or gradient penalties could prevent mode collapse and help the GAN generalize its fooling ability to truly unseen attacks.

# Helpful Links
Notebook: 
[ML_Project.ipynb](XXX)

Video: 
[ML_Video.mpg](xxx)

Executive Report:
[ML_Executive_Report.pdf](xxx)

# Dataset
Dataset Used: 
[Thursday-WorkingHours-Morning-WebAttacks.pcap_ISCX.csv](https://drive.google.com/file/d/1BLHP9C-UINGtOlxfoTMAlhoTSzVo1Krr/view?usp=sharing)

# Weights 
Weight Directory:
[WEIGHTS_DIR](https://drive.google.com/drive/folders/10APGxnjOU0gR5EPhaeEShh7HKdHA-krB?usp=sharing)

Model Path:
[xgb_weights.pkl](https://drive.google.com/file/d/1PlUvsRigILkn2RyetRPfqrWSdkBFzJ6j/view?usp=drive_link)

Scaler Path:
[scaler_weights.pkl](https://drive.google.com/file/d/101iRWSn149wfjJ42SZ0hfeG0fon76_4X/view?usp=sharing)

ENC Path:
[label_encoder_weights.pkl](https://drive.google.com/file/d/13aeCtGmtadMzaKNv3GG6Vz-NK68oE4kT/view?usp=sharing)

Fake Path: 
[gan_fakes.pkl](https://drive.google.com/file/d/1FqVlcgCRvP_IGGg6fj8VgZuOdIeqlrfg/view?usp=sharing)

Augmented Data Path: 
[augmented_data.pkl](https://drive.google.com/file/d/1QbGsjUUAT4blhsOcIK7PqLqL00UmUvsH/view?usp=sharing)

Generator Data Path: 
[generator.pth](https://drive.google.com/file/d/1AACB3otpgyAIf9z7qNaqyVm4VN5H6xTH/view?usp=sharing)

Generator Weights Path: 
[generator_weights.pth](https://drive.google.com/file/d/1klHZ4uKpDKWtPdR7HTUYMgdJNtF1aIER/view?usp=sharing)

Discriminator Data Path: 
[discriminator.pth](https://drive.google.com/file/d/1f6fSs6czUOuJyvlmxjX3oyFqbSGOjUGe/view?usp=sharing)

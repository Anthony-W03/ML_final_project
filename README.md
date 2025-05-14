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
After running the defender model, we generated a confusion matrix, which shows that it does an excellent job at classifying Benign traffic and a pretty good job at figuring out if data is malicious, but struggles in actually classifying between different types of attacks. Due to the small percentage of our data that were actually attacks, we expected our model to struggle with differentiating between them, with the biggest culprit being between XSS and Brute force attacks. Overall, while our model is good at detecting when it is being attacked, it currently isn’t the best at classifying the attack correctly. 
	Through running the attacker model, the GAN model learns to trick our XGBoost defender very quickly as its surrogate loss falls from 0.62 to 0.54 in just a few epochs, and by epoch 20 it can fool the defender 100% of the time on its training batch—but this success is brittle. The discriminator and generator losses swing wildly throughout training, and the fooling rate plunges back down (to as low as 9%) before rebounding, showing the model overfits and then forgets. A t-SNE plot confirms that the fake flows cluster separately from real attacks, so although the GAN exploits the defender’s blind spots, it does so with unrealistic, unstable samples rather than true adversarial replicas. Overall, the GAN can fool the defender on seen data, but its unstable, unrealistic samples won’t hold up in real use.

# Helpful Links
Notebook: 
[ML_Project.ipynb](ML_Executive_Report.pdf)

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

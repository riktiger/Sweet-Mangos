AN AUTOMATIC HYPERPARAMETER TUNING APPROACH TO DISEASE DETECTION IN MANGO TREES USING TRANSFER LEARNING-BASED CONVOLUTED NEURAL NETWORKS
**************************************************************************************************************************************

BACKGROUND: Mango is a tropical fruit that originated from the Southern Asia region. The fruit is high in vitamins and nutrients and a rich source of vitamins A and C. The fruit is consumed all over the world in fresh, frozen as well as processed forms. Manufacturers will use it to make confectionary and processed food items. Mangoes offer plenty of health benefits as they contain [vitamin C](https://www.databridgemarketresearch.com/reports/global-vitamin-c-market), an immune-boosting antioxidant that helps fight cancer and other diseases and complications. Mangoes help keep eyes and skin looking healthy as they contain vitamin A and keep the digestive system in good health by providing plenty of fiber. Moreover, mangoes contain potassium, which helps to regulate blood pressure.
The major factor likely to support the growth of the global mango market is the increased product demand from the beverage industry. Various large-scale food and beverage producers have introduced products based on mango into the market, such as Starbucks, McDonald's, and PepsiCo, among others. Mango puree or the refined pulp of the fruit is mostly used to make juices, nectars, drinks, jams, fruit, cheese, and other beverages. It is also used in puddings, bakery fillings, fruit meals for children, flavors for the food industry, and ice creams, yogurt, and confectionery items. With the rapid urbanization and increasing disposable income in developing countries, the consumer is inclined towards convenient food products such as ready-to-eat food and ready-to-drink beverages. Food manufacturers are shifting their focus to ready-to-eat products to serve the increasing demand for convenient food products.
The increasing government initiatives and research and development work for mango production is a major market opportunity. However, seasonal availability and high pest and disease attack may hamper the market growth. Hence, there is a requirement for developing an easy-to-use methodology to inspect the various diseases that can damage production.


AIM: To develop an easy-to-use image-based disease detection algorithm for mango trees.


METHODOLOGY:

DATASET:

Prepared by Ali, Sawkat; Ibrahim, Muhammad; Ahmed, Sarder Iftekhar; Nadim, Md.; Mizanur, Mizanur Rahman; Shejunti, Maria Mehjabin; Jabid, Taskeed (2022), “MangoLeafBD Dataset”, Mendeley Data, V1, doi: 10.17632/hxsnvwty3r.1
Contains 4000 images of mango leaves each with a resolution of 240x320. Of these, around 1800 are of distinct leaves, and the rest are prepared by zooming and rotating where deemed necessary. They are of the Jpeg format and taken at four mango orchards in Bangladesh, namely Sher-e-Bangla Agricultural University orchard, Jahangir Nagar University orchard, Udaypur village mango orchard, and Itakhola village mango orchard. Images were shot using a mobile phone. The entire dataset was downloaded from Kaggle [[Mango🥭 Leaf🍃🍂 Disease Dataset | Kaggle](https://www.kaggle.com/datasets/aryashah2k/mango-leaf-disease-dataset)].
It contains images of healthy mango leaves and 7 classes of leaves infected with common diseases. These include Anthracnose, Bacterial Canker, Cutting Weevil,  Die Back, Gall Midge, Powdery Mildew, and Sooty Mould.

![image](https://github.com/riktiger/Sweet-Mangos/assets/57993082/630a35dd-0d89-4abf-afea-0100784b7b0e)

It was decided for the final implementation 90% of the total data would be used for training and validation and 10 % would be used for testing. 20% of the training set would be used for validation.

![image](https://github.com/riktiger/Sweet-Mangos/assets/57993082/e075049b-823c-43c1-8fd2-66fa02ff461e)

However, during the initial automatic hyperparameter tuning process, about 90% of the total training data was used in the hyperparameter tuning training process, and the remaining 10% was for Validation. This was mainly done since Validation accuracy was the target objective during the hyperparameter tuning process using RandomSearch with Keras-Tuner

![image](https://github.com/riktiger/Sweet-Mangos/assets/57993082/2c833928-bc77-44fb-9ad9-62d382822ded)


IMPLEMENTATION OF THE CONVOLUTIONAL NEURAL NETWORK

The Xception Model from Keras applications was used as the base for the CNN used in this project. This was chosen for two reasons: 1) During the development of the CNN, the Xception was not used by anyone (on Kaggle) and thus would give an indication of the performance of Xception on this dataset 2) Xception offers very high accuracy (Top-1 Accuracy: 79.0%   Top-5 Accuracy: 94.5% ) for a relatively low number of parameters (22.9M) and low overall depth (81 layers)
The top layer was removed and the layers within Xception were made untrainable with the weights used from imagenet. Input shape was kept at the default (299,299,3). To this, custom layers were added and optimization and selection of the best hyperparameters were performed with Keras – Tuner and Random Search.
The tuning operation was performed with Kaggle with the P100 GPU. A total of 50 trials to select the best hyperparameters was made, each trial running for 6 epochs. The model generating the highest validation accuracy was selected.

The final structure of the implemented model came out to be

![image](https://github.com/riktiger/Sweet-Mangos/assets/57993082/904dc539-24ec-4767-a97d-c0843c9f3cee)

![image](https://github.com/riktiger/Sweet-Mangos/assets/57993082/9f6097e6-199e-4e89-b156-573c322d132e)

Optimizer = Adam (Learning Rate =0.001)    Loss=Categorical Cross Entropy      Metrics=Accuracy


IMAGE AUGMENTATION

![image](https://github.com/riktiger/Sweet-Mangos/assets/57993082/65f9c0bd-4b52-4f40-abc5-d1279de13a91)


TRAINING RESULTS AFTER 100 EPOCHS AT A BATCH SIZE OF 32

![image](https://github.com/riktiger/Sweet-Mangos/assets/57993082/6555c496-06f9-497b-a581-daaa12b17498)

![image](https://github.com/riktiger/Sweet-Mangos/assets/57993082/4364d08f-0153-4187-b9de-b8eebd371810)


TEST RESULTS

![image](https://github.com/riktiger/Sweet-Mangos/assets/57993082/099abbc4-ef3b-4917-9e60-175dcaa48223)





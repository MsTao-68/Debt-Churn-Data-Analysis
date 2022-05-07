# Churn Data Analysis
使用比赛方提供的脱敏数据，进行客户信贷流失预测。**根据比赛方要求，无法开源数据。**

- [x] Version 1: CMTR_CHURN_PR 传统机器学习 **XGBoost** 
  - AUC: 0.6145
------
- [x] Version 2: CMTR_CHURN_PR_V2 人工神经网络 **ANN**
  - 遇到的问题：
    1. 做了特征工程，发现变量的相关性与是否流失基本不相关，而变量之间的相关性显著，即是否去除变量，对AUC和准确率影响不大。
      - 解决思路：使用人工神经网络。
        1. 损失函数：model.compile(loss='binary_crossentropy', optimizer='adam', metrics=['accuracy'])
          - 两层全连接层：AUC: 0.75 | Score：0.8335148392539795
          - DNN（五层）: AUC: 0.8424366624721034 | Score: 0.8074
        2. 损失函数：model.compile(optimizer='adam', loss='mean_squared_error', metrics=['accuracy']) |  validation_split=0.2
          - 两层全连接层：AUC: 0.8424366624721034 | Score: 0.8452
          - DNN（五层）: 0.8764842415303271 | Score: 0.8323
        3. 总结：人工神经网络效果不如XGB，通过损失函数绘图发现有过拟合现象，验证集效果远不及训练集。
-----
- [x] Version 3: CMTR_CHURN_PR_V3_ TabNet 使用无监督模型进行预训练 
  - 遇到的问题：AUC和准确率提升依旧很难，模型效果比较差。AUC: 0.6511318268787747 | Score: 0.74
    - 解决思路：使用PCA主成分分析法，进行特征降维, 准确率依旧下降，出现特征工程无效的情况，原因未知。AUC: 0.5801404503216607
-----
- [x] Version 4: CMTR_CHURN_PR_V4 变量分箱 | XGB | RF | TabNet | AutoML
  - 经过特征选择后（TOP30），对字符型变量进行独热编码，对数值型去除量纲，并进行等间距分箱，num_bins = 6
    1. XGB: AUC: 0.6046600198503995 | Score: 0.775887943971986
    2. RandomForest: AUC: 0.6046600198503995 | Score: 0.7712606303151576
    3. TabNet 无监督预训练， AUC: 0.7872822945848122
    4. AutoGluon 直接输出leaderboard，并使用TOP3的模型进行预测。




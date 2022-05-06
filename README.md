# Debt-Prediction-Classification
使用比赛方提供的脱敏数据，进行客户信贷流失预测。**根据比赛方要求，无法开源数据。**
Request data, please contact me by e-mail: brainiac_tra09@qq.com
- [x] Version 1: CMTR_CHURN_PR 传统机器学习 **XGBoost** 
  - AUC: 0.9743255659575887
  - Score: 0.9296077646587952
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




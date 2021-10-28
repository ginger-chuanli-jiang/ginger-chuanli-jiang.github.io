# Notes about Random Forests

### Random Forest:

Random Forest is an ensemble learning method used for classification and regression. It combines Breiman's bagging sampling approach and the random feature selections originated by Ho 1995 and 1998. In the original paper on RF, Breiman showed that the RF error rate depends on correlation and strength. Increasing the correlation between any two trees in the RF increases the forest error rate. Increasing the strength of the individual trees decreases the RF error rate.

Specifically, suppose we have N training samples, and M features. First, we do bootstrapping sampling N times to select N samples, then for each node, we randomly select features (the number of features should be less than the total number of features). Determine the best spliting based on Gini index and cross entropy. Each tree is allowed to grow without any pruning. 

Mean feature importance can be calculated in RF by averaging the gini decreases for each individual feature over all trees in the forest. This metric, sometimes, can be unreliable. Permutation importance can therefore be computed by calculating the difference between a baseline accuracy (classification) or R2 (regressor) and the drop in overall accuracy or R2 by permuting the feature.

Key advantages of RF over its Adaboost counterpart are robustness to noise and overfitting. RF is very fast in both training and classification. Second, RF can be easy parallelized, which makes it interesting for multi-core and GPU implementations. RF is suitable for multi-class prediction.

Several studies have replaced Breiman's majority voting with weighted voting, more sophisticated dynamic integration techniques such as Dynamic Selection, Dynamic Voting, and Dynamic Voting with Selection, and hybrid algorithm. 

Online random forest was developed by Saffari et al., 2009. The on-line RF has to combine on-line bagging and on-line decision trees with random feature-selection.

### Ensemble Classification:

Ensemble classification is an application of ensemble learning to improve the accuracy of classification. Ensemble learning is a machine learning approach to solve a prediction problem by using multiple models. In ensemble classification, multiple classifiers are used to achieve better accuracy than the individual classifier in the ensemble. A voting scheme is then used to determine the final class label for prediction. 

### Voting:
A simple but effective voting scheme is majority voting (Lam and Suen, 1997). In majority voting, each classifer in the ensemble is used to predict the class label, then the class that receives the greatest number of votes is returned as the final decision of the ensemble.

An alternative voting scheme is veto voting (Shahzad &amp; Lavesson, 2012; Sun &amp; Dance, 2012). In veto voting, one single classifier vetoes the final decision of other classifiers. 

Trust-based veto voting is an extention of veto voting scheme (Shahazad and lavesson 2013). In trust-based veto voting, the trust (weights) of each classifier is used to determine whether one single classifier or a set of classifiers can veto the final decision. 

### Boosting, Bagging, Stacking:

Ensemble learning usually includes three approaches to aggregate final decisions, they are boosting, bagging, and stacking. 

Boosting is an incremental process of building a sequence of classifiers, where each classifier works on the incorrectly classified instances of the previous one in the sequence. AdaBoost (Freund &amp; Schapire, 1997) is the representative of this class of techniques. AdaBoost is prone to overfitting. 

Bagging is a bootstrap aggregating process of building each classifer in the ensemble using a randomly drawn sample of the samples, having each classifier contributes equally to the final class label (Breiman, 1996). Random Forest (RF, Breiman, 2001) is the main representative of bagging. Bagging is robust than boosting against overfitting.  

Stacking is an extendtion of cross-validation technique, where the data set is partititioned into a held-in data set and held-out data set, and the held-in data is used to train the models, and the best performing model is selected on the held-out data for prediction. 

### References:

Kahled Fawagreh, Mohamded, Medhat Gaber, Eyad Elya
RF: From Early Developments to Recent Advancements
System Science And Control Engineering, 2 (1) (2014), pp. 602-609

Lam, L. and Suen, C.Y. (1997) Application of majority voting to pattern recognition: An analysis of its behavior and performance. IEEE Transactions on Pattern Analysis, 27, 553-568.

Amir Saffari, Christian Leistner, Jakob Santner, Martin Godec, and Horst Bischof, “On-line Random Forests,” in 3rd IEEE ICCV Workshop on On-line Computer Vision, 2009.

Khaled Fawagreh, Mohamed Medhat Gaber & Eyad Elyan (2014) Random forests: from early developments to recent advancements, Systems Science & Control Engineering, 2:1, 602-609, DOI: 10.1080/21642583.2014.956265

Shahzad, R. K., & Lavesson, N. (2012). Veto-based malware detection. In 2012 seventh international conference on availability, reliability and security (ARES), Prague, Czech Republic (pp. 47–54). New York City, NY: IEEE

Sun, Y.-A., & Dance, C. (2012). When majority voting fails: Comparing quality assurance methods for noisy human computation environment. CoRR. Retrieved from arXiv:1204.3516. 

Shahzad, R. K., & Lavesson, N. (2013). Comparative analysis of voting schemes for ensemble-based malware detection. Journal of Wireless Mobile Networks, Ubiquitous Computing, and Dependable Applications, 4(1), 98–117.

Freund Y., & Schapire, R. E. (1997). A decision-theoretic generalization of on-line learning and an application to boosting. Journal of Computer and System Sciences, 55(1), 119–139. doi: 10.1006/jcss.1997.1504

Breiman, L. (1996). Bagging predictors. Machine Learning, 24(2), 123–140. 

Breiman, L. (2001). Random forests. Machine Learning, 45(1), 5–32. doi: 10.1023/A:1010933404324

Ho, T. K. (1995). Random decision forests. In Document analysis and recognition, 1995, Proceedings of the third international conference, Montreal, Quebec, Canada (Vol. 1, pp. 278–282). New York City, NY: IEEE. 

Ho, T. K. (1998). The random subspace method for constructing decision forests. Intelligence, IEEE Transactions on Pattern Analysis and Machine, 20(8), 832–844. doi: 10.1109/34.709601 

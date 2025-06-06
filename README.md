# **Directed Graphical Models**

**Implementing** and **experimenting** with directed graphical models using **"medical domain"** data.

### **Medical Domain Data**

You are provided with a **joint probability distribution** of  **symptoms** ,  **conditions** , and  **diseases** . Certain diseases are more likely than others given certain symptoms, and a model such as this can be used to help doctors make a  **diagnosis** . The ground-truth joint probability distribution consists of **twelve binary random variables** and contains **2^12 possible configurations** (numbered  **0 to 4095** ), which is small enough that you can enumerate them exhaustively.

The variables are as follows:

* **(0) IsSummer** : **True** if it is the summer season, **False** otherwise.
* **(1) HasFlu** : **True** if the patient has the flu.
* **(2) HasFoodPoisoning** : **True** if the patient has food poisoning.
* **(3) HasHayFever** : **True** if the patient has hay fever.
* **(4) HasPneumonia** : **True** if the patient has pneumonia.
* **(5) HasRespiratoryProblems** : **True** if the patient has problems in the respiratory system.
* **(6) HasGastricProblems** : **True** if the patient has problems in the gastro-intestinal system.
* **(7) HasRash** : **True** if the patient has a skin rash.
* **(8) Coughs** : **True** if the patient has a cough.
* **(9) IsFatigued** : **True** if the patient is tired and fatigued.
* **(10) Vomits** : **True** if the patient has vomited.
* **(11) HasFever** : **True** if the patient has a high fever.

The **medical.zip** file contains two files:

* **joint.dat** : The **true joint probability distribution** over the twelve binary variables. Since each variable is binary, we can represent a full variable assignment as a  **bitstring** . This file lists all **2^12 assignments** (one in each line) as pairs **"Integer Probability"** where **"Integer"** is an integer encoding of the bitstring. Specifically, assuming **False=0** and  **True=1** , an assignment to all variables results in a **12-bit binary number** (with the index of the variables shown in parentheses above) which is converted to a decimal number. For example, assignment **0** represents all variables are  **False** , **1** represents only **IsSummer** is  **True** , **2** represents only **HasFlu** is  **True** , and so on.
* **dataset.dat** : The dataset consists of **samples** from the above probability distribution. Each line of the file contains a **complete assignment** to all the variables, encoded as an **integer** (as described above).

### **Core Tasks**

1. **Graphical Model** : Use your intuition to design a **directed graphical model** for the twelve variables outlined above. Implement it in the  **programming language of your choice** . You could begin your implementation work using simply  **randomly-assigned parameters** . Given these parameters, and an assignment to  **12 of the variables** , your implementation should be able to return the  **probability of the full assignment** .
2. **Estimating Parameters** : Use the dataset (i.e.,  **dataset.dat** ) to estimate the **parameters** of your graphical model. You can do this by simply  **counting and normalizing** , i.e., enumerate all the assignments in the dataset, and for each variable  **v** , count the number of times a variable is **True** for each assignment to its  **parents** , and then normalize the counts using the **total number of times** the parents had that assignment
3. **Model Accuracy** : Measure the **similarity** of your model to the **true joint probability distribution** (i.e.,  **joint.dat** ). That is, for each assignment, how similar are the probabilities returned by your model to the  **true probability distribution** . To keep things simple, you can compare the distributions based on their  **L1-distance** . That is, for each assignment **a_i** to all the variables, obtain **p(a_i)** from the true joint distribution (( **i+1** )th row in  **joint.dat** ) and **p(a_i)** using your model. The distance is defined as  **|p(a_0)-p(a_0)| + |p(a_1)-p(a_1)| + ... + |p(a_4095)-p(a_4095)|** . An alternative distance measure more appropriate to probability distributions is  **KL-divergence** . If you know what that is, and want to use it, you can evaluate using **KL-divergence** also.
4. **Querying** : Use the graphical model above to answer some  **queries** . A query consists of **observed variables** (for which we have an assignment), and **query variables** that over which we want the  **distribution** . The remaining variables need to be **marginalized** (by summing them out). Since the domain is small, you can implement this **conditioning** and **marginalizing** process by **exhaustively enumerating** all assignments (note that only assignments that are **consistent** with the observed values should be taken into account). Compare the results of these queries on your model to results obtained from using the  **true joint probability distribution** . Try to think of some **interesting queries** that will demonstrate  **causal reasoning** ,  **evidential reasoning** , and  **inter-causal reasoning** . To get you started, here are some examples of queries to consider (but also create new ones of your own design):

---



* What is the **probability** a patient has **flu** given they are **coughing** and have a  **high fever** ? ( **Observed Variables** :  **HasFever=True** ,  **Coughs=True** ;  **Query Variable** :  **HasFlu** )
* What is the **probability distribution** over the **symptoms** ( **HasRash** ,  **Coughs** ,  **IsFatigued** ,  **Vomits** , and  **HasFever** ) given the patient has  **pneumonia** ?
* What is the **probability** of **vomiting** in  **summer** ?

### **What to Hand In**

* You should provide a **short (1-3 page) report** describing your **explorations** and  **results** . Include a description of the **graphical model** you implemented (e.g., a  **diagram** , or a list of **parents** and **conditional probabilities** of the form:  **p(a|b,c,...)** ). Discuss the **compactness** (how many parameters does your model use?) and **accuracy** (how close were you to the  **true joint probability distribution** ?) of your model. Discuss your experiences in writing the **query-implementing code** and the **queries** your model was used to answer. Also include details of the **optional tasks** you did.
* Include the **complete source code** of your implementation.

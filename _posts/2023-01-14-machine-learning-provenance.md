## Machine Learning Provenance
![Bottle of wine in antique shop](/images/Bottle of wine in antique shop 2.jpeg)
During my six plus years working professionally in machine learning I’ve come across several key mistakes that people in machine learning (and I!) make early in their careers. I’m not talking about the very simple mistakes that we make during our first few months of learning machine learning in college or elsewhere. I'm talking more about the mistakes you make a few years into your career. The mistake I want to talk about is this: ending up in a state where you are unable to trace an inference back to the model that produced it, and/or being unable to trace a model back to its training data.

### Provenance
If I were to express what this concept is in a single phrase it would be machine learning provenance. Provenance refers to origins of something and how it came to be where it is today. This is a fundamental thing. If you are unable to trace an inference back to the model that produced it you are unable to reproduce the results. Similarly, if you are unable to say what data was used to train the current model, how would you go about training an updated version of the model should some kind of concept or data drift occur and retraining were necessary?

![confused Robot butler pouring wine impressionist painting](/images/confused Robot butler pouring wine impressionist painting.jpeg)
### Model Provenance
How many times have you had a great model, but you don't remember the details of how you finally came to produce that final product months or years later? You’ll probably remember the architecture and framework used, and maybe some details about the dataset, but even if you have a training script in version control are you sure that version was the one used to train the model that made it into production, or was it one of the other similarly named training scripts? If you find yourself in this scenario you’ll know you should have done something better the first time, but what would that be?

Good model provenance is having the following information easily accessible to any who need to use it:
- Unique model ID, possibly a version ID as well
- Training start and end times, any other useful timestamps
- Description and possibly name
- Information on the datasets used in training (I prefer having a dataset ID that links to a separate database for datasets so dataset and model metadata are not coupled)
- Framework (e.g. Pytorch, Sklearn) and its version used for training
- Locations of all assets (.pt file, etc.)
- Hyperparameters
- Training script or module
- Training results like dev set evaluation metrics
- Whatever else you need for your use case

Having good model provenance means you should always be able to attribute an inference to a model, and be able to know enough about that model to answer any questions you may need to in the future. You should also be able to reproduce your model if needed. The most likely scenario being training on a newer or larger dataset. 

### Model registry
The simplest way to accomplish having good model provenance as laid out in the previous section is to use an MLOps tool called the model registry. The model registry gives you a way to  keep track of every model in production (and even those in development). The model registry should also know where each of the assets for any given model are and keep track of all its metadata. This should all be available to other APIs and engineers via an API.

The model registry I built at Drift is a fastAPI service with a MySQL RDS instance and an accompanying bucket in S3 which houses all the model artifacts in the registry. We use the registry for our flagship conversational AI product at Drift and so far it has scaled well. The registry receives on average a few hundred requests per minute, and around 15k requests per minute during peak times. Its ability to scale well is no doubt by virtue of it being a Kubernetes service.

![confused Robot butler pouring wine impressionist painting](/images/confused Robot butler pouring wine impressionist painting2.jpeg)
### Data Provenance
There are a few situations in which it is apparent that good data provenance is essential. One is the typical case in which you find you need to retrain your model. This could be for any number of reasons. Maybe a new base model came out, and you want to try fine-tuning this new model using an existing dataset you have. Let's say in this scenario that for your existing fine-tuned model you used a proprietary data set that your company owns, and let's say that maybe you even know what dataset you originally used. But maybe you did some data wrangling, and maybe you wanted to get it done quickly so that you could get to the modeling so that you could get to the fun part. I think we've all done something like this. You start cleaning up the data in a Jupyter notebook, and you end up exporting the data to a JSON file somewhere and do some benchmarking, and after that you find that you needed to bring in another data source, or you needed to do some other preprocessing of the data. So you export another JSON file, and soon enough you've got five files, and you're not sure which one of them you ended up using for fine-tuning your existing model. Hopefully you're able to figure out which one of these to use or be able to otherwise recreate the results you're able to get before with the new base model.

The other situation in which you need data provenance might be a legal or ethical scenario (but there could still be some other reason). Let's say that for some reason you found out that all data from source X was unusable for training purposes. Unless you have good data provenance you won't be able to say whether or not your model was trained on any data from source X. This may lead to costly preprocessing of the data and retraining of any models where source X may have been used. On the other hand this  wouldn't be a problem for a ml organization with good model development and deployment practices. They will simply look up the model in the model registry and be able to track down the training data, and definitively say whether source X was used in training this model or not. Ideally they’d be able to definitely say which training examples specifically are from source X.

### Dataset registry	
This tool goes by different names, but I prefer to call it a data set registry because I see it as someone analogous to the model registry. Essentially, the purpose of this tool is to give you a  way to track data sets. This isn't as cut and dry as keeping a model registry for one reason, a model is atomic whereas a data set can be divided up. Also, you can change one or two things about the data set without changing anything else, but if you change one thing about a model you change everything so if there's a new model that should have a new model version ID.

The simplest thing to do would be to copy this model registry design pattern and for every change you make to a data set you save out an entirely new copy of the data, and you give that new data set a new version ID. However, of course, this is extremely inefficient. There's going to be a whole range of solutions in between doing something like this and doing something very clever and efficient, but more clever solutions are going to take far more clever engineering and likely more maintenance. So in this case I would suggest going with an existing tool for data set management rather than building your own unless you have a good reason to do so. The dataset registry product I’ve been most impressed with thus far is [DVC](https://dvc.org/doc/use-cases/data-registry) (standing for Dataset Version Control). DVC is an open source solution that is built on top of Git.

![confused Robot butler pouring wine impressionist painting](/images/confused Robot butler pouring wine impressionist painting3.jpeg)
### Summing things up
Two of the most important things to remember when using machine learning in production are to make sure you have a way to trace every inference back to its model, and make sure you can trace every model back to the data that it used in training. Two tools that can help you with this are the model registry and the dataset registry (AKA dataset version control).

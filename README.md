# AI Deep Learning Web Site

Organization's web site deployed using GitHub Pages.

[AI Deep Learning](https://huggingface.co/ai-deep-learning) Hugging Face organization.

## What has been done

* Created an AWS account
* Created an AWS organization
* Granted access to Giri
* Initial basic set up of SageMaker
* Created GitHub organization
* Configured organization's domain and initial web site - https://ai-deep-learning.us/
* Researched AWS instance types for deep learning, P4 are fastests and most economical, but most expensive per hour at the same time - $30/hour
* Requested access to SageMaker Studio Labs

## Next steps

* Set up local environment for StarCoder - https://github.com/bigcode-project/starcoder/tree/main
* Figure out the best way to run StarCoder on AWS (EC2, ECS, spot instances?), implement, document


## Resources

* https://github.com/bigcode-project/starcoder/tree/main
* https://github.com/huggingface/text-generation-inference
* https://huggingface.co/chat
* https://aws.amazon.com/blogs/aws/managed-spot-training-save-up-to-90-on-your-amazon-sagemaker-training-jobs/
* https://github.com/aws/amazon-sagemaker-examples
* https://docs.aws.amazon.com/sagemaker/latest/dg/studio-ui.html
* https://sagemaker-examples.readthedocs.io/en/latest/aws_sagemaker_studio/getting_started/xgboost_customer_churn_studio.html
* https://docs.aws.amazon.com/sagemaker/latest/dg/gs-studio-end-to-end.html
* https://docs.aws.amazon.com/sagemaker/latest/dg/studio.html
* https://docs.aws.amazon.com/sagemaker/latest/dg/nbi.html
* https://aws.amazon.com/blogs/machine-learning/ensure-efficient-compute-resources-on-amazon-sagemaker/
* https://docs.aws.amazon.com/sagemaker/latest/dg/notebook-lifecycle-config.html
* https://aws.amazon.com/machine-learning/elastic-inference/
* https://aws.amazon.com/blogs/machine-learning/amazon-sagemaker-automatic-model-tuning-now-supports-early-stopping-of-training-jobs/
* https://aws.amazon.com/blogs/machine-learning/optimizing-costs-for-machine-learning-with-amazon-sagemaker/
* https://aws.amazon.com/free/machine-learning/
* https://docs.aws.amazon.com/deep-learning-containers/latest/devguide/deep-learning-containers-ecs-tutorials-inference.html
* https://docs.aws.amazon.com/deep-learning-containers/latest/devguide/deep-learning-containers-ecs-tutorials-training.html
* https://docs.aws.amazon.com/deep-learning-containers/latest/devguide/deep-learning-containers-ecs-setup.html
* https://docs.aws.amazon.com/deep-learning-containers/latest/devguide/deep-learning-containers-images.html
* https://docs.aws.amazon.com/sagemaker/latest/dg/docker-containers.html
* https://docs.aws.amazon.com/deep-learning-containers/latest/devguide/deep-learning-containers-ecs.html
* https://aws.amazon.com/machine-learning/containers/
* https://aws.amazon.com/getting-started/hands-on/train-deep-learning-model-aws-ec2-containers/
* https://docs.aws.amazon.com/sagemaker/latest/dg/whatis.html
* https://colab.research.google.com/notebooks/ - gives 12 Gb of RAM and 100 Gb of disk. Upgrades available - https://colab.research.google.com/signup/pricing. T4 GPU available in the free tier, A100 and V100 available in premium tiers. A100 is 1.6x - 3.4x faster than V100. A100 is ~ 5x to 10x faster than T4
* Anaconda in the cloud - https://www.anaconda.com/code-in-the-cloud - 100 Mb of cloud storage, 500 seconds/day of hight compute. Pricing - https://www.anaconda.com/pricing/individuals
* https://huggingface.co/docs/transformers/sagemaker
* https://github.com/huggingface/notebooks/tree/main/sagemaker
* https://huggingface.co/pricing - compute for AI
* https://aws.amazon.com/machine-learning/mlu/

## Pavel's local 

* RAM: 16 Gb
* GPU: NVIDIA GeForce GTX 980
    * 12 Gb RAM, 
    * 5 TFLOPS vs 65 TFLOPS on T4 (Google Colab Free tier) and 312/624 TFLOPS on A100 (Premium Tier). T4 is 13x faster, A100 is 62x faster

## Local setup

* Install Anaconda - https://www.anaconda.com/download
* Open Anaconda prompt
* Create environment: ``conda create -n star-coder python=3.11``
* Activate environment: ``conda activate star-coder``
* Install Hugging Face CLI: ``pip install --upgrade huggingface_hub`` (this step is in the online instructions. However, the CLI also gets installed as part of requirements installation) 
* Clone StarCoder: ``git clone https://github.com/bigcode-project/starcoder.git``
* CD to the starcoder directory
* Install requirements: ``pip install -r requirements.txt``
* Generate a read access token for Hugging Face: https://huggingface.co/settings/tokens
* Login to hugging face: ``huggingface-cli login``
* Install jupyter: ``pip install jupyter``
* Start jupyter notebooks: ``jupyter notebook``

It my setup it was giving strange errors about not sufficient memory - unable to allocate 150 Mb and 600 Mb with several Gb available. It happened in both GPU and CPU modes so I suspended by efforts to run it locally.

## SageMaker

Set disk size to 150 Gb

* Create a notebook on ml.t3.medium - 250 hours/months are provided for free for the first 2 months. Customize to have 150 Gb storage
* Open a JupyterLab
* Go to terminal and create a symbolic link from`` ~/.cache/huggingface`` to ``/home/ec2-user/SageMaker/.cache/huggingface``. This is needed to have enough space for cache (~80 Gb)
    * ``sh-4.2$ mkdir /home/ec2-user/SageMaker/.cache``
    * ``sh-4.2$ mkdir /home/ec2-user/SageMaker/.cache/huggingface``
    * ``sh-4.2$ chmod 777 /home/ec2-user/SageMaker/.cache/huggingface``
    * ``sh-4.2$ ln -s /home/ec2-user/SageMaker/.cache/huggingface .cache/huggingface``
* Open a notebook
* Install requirements from requirements.txt using pip: ``%pip install tqdm transformers datasets huggingface-hub accelerate``
* Install sagemaker ``%pip install sagemaker --upgrade``
* Login to Hugging Face from terminal ``huggingface-cli login --token <your token here>``
* Open a notebook
* Run the first snippet from starcoder

## Notes

StarCoder requires ~80 Gb of disk space. As such it cannot be run on Google Colab free tier as is provides "only" 78.2 Gb disk space.

## SageMaker Studio Lab

https://studiolab.sagemaker.aws - requires approval. 

GPU compute - 4 hours per session and 8 hour in 24 hours period. Storage is limited to 15 Gb



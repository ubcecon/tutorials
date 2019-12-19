# Rough Notes for AWS

## Images for EC2
 
- Matlab on AWS EC2: https://github.com/mathworks-ref-arch/matlab-on-aws
  - More general matlab on docker: https://github.com/mathworks-ref-arch/matlab-dockerfile?s_eid=pep_ghubrefmldocker
  - https://github.com/mathworks-ref-arch  has a lot
- Stata: https://ck37.com/post/stata-windows-amazon-ec2-guide/
- Jupyter: https://d1.awsstatic.com/WWPS/pdf/AWS_Jupyter_Instance_Whitepaper_v6.pdf
- See the [AWS Educate](https://aws.amazon.com/education/awseducate/) program
  - $100 in AWS Promotional Compute Credit per student or $200 per faculty per year.
  - Access to training materials
- https://aws.amazon.com/image-builder/  is a new tool for building images.  Uses an Image Builder recipe?
- Advice was to use the Amazon Deep Learning AMI - which has cuda/etc. already steup.  Just add Julia.
  - See https://aws.amazon.com/blogs/machine-learning/get-started-with-deep-learning-using-the-aws-deep-learning-ami/

## S3
= Mount bucket on EC2 instance: https://medium.com/tensult/aws-how-to-mount-s3-bucket-using-iam-role-on-ec2-linux-instance-ad2afd4513ef

## EC2

- For your own virtual server in the cloud, you would use [EC2](https://aws.amazon.com/ec2/)
  - Free: 750 hours per year of small instances.  See https://aws.amazon.com/free/
  - For paying, choose how much computing you need (e.g. https://aws.amazon.com/ec2/instance-types/) and the prices are often spot market prices in various locations
- You base your instance off of an "image" with a particular operating system.  e.g. Windows, Debian, etc.
  - All sorts of additional images in the https://aws.amazon.com/marketplace
  - Instances can also have stuff preloaded, we would just need to find nice ones.  e.g. probably datascience images/etc.?
  - I think you can add features to the base images easily.  e.g. Add [CUDA](https://aws.amazon.com/marketplace/pp/B01LZMLK1K?qid=1575522727903&sr=0-2&ref_=srh_res_product_title)
  - It would be helpful for a research engineer to play around and find good "datascience" etc. images.
- With it, you only pay for time you are actively running it, and can choose to hibernate/pause.
   - If you pause, I think you only pay for the (dirt-cheap) storage of the image.
- Also, you could come up with your own container image and store it for quick access with https://aws.amazon.com/ecr/

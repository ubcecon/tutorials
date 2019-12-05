# Rough Notes for AWS

- See the [AWS Educate](https://aws.amazon.com/education/awseducate/) program
  - $100 in AWS Promotional Compute Credit per student or $200 per faculty per year.
  - Access to training materials

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

## Fargate
For many use-cases (e.g. estimation) you do not need to have an interactive server and just want to run a batch job.  Consider using a container instead of a virtual server.

- The server-less container solution is [Fargate](https://aws.amazon.com/fargate/)
- If we used it, I think we could come up with some standard container images (or use existing ones)
  - Then the scripts could download data/code/etc. and run it as part of the container bootup
  - e.g. use one of the https://github.com/jupyter/docker-stacks images
- The downloading/etc. into the container could happen through github access to the code repository, and then data could be mounted on AWS storage
- The major benefit of this, besides reproducibility, is that the container can run on cheap spot instances
  - So the pricing could be dramatically lower!
  - Furthermore, I think that it may elastically expand RAM and cores as you use them?  That is ideal for our tasks.
  - https://aws.amazon.com/fargate/pricing/?nc=sn&loc=2
- If you are running complicated and non-interactive jobs, then this seems like the winning solution - if we can figure it out.
- Also, you could come up with your own container image and store it for quick access with https://aws.amazon.com/ecr/
- Can you handle proprietary data?  Of course.  This stuff is even HIPA compliant/etc.  Whether that should be built into the image or not, I don't know.

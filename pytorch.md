# PyTorch and PyTorch Lightning

General advice:
- Use PyTorch Lightning to organize your codde
- If you use lightning, you will not need to worry about GPU-specific code and devices
- Use an ArgumentParser to add in all of the Lightning options without having to code them.
  - See https://pytorch-lightning.readthedocs.io/en/latest/introduction_guide.html#argparser-best-practices

## Learning PyTorch Lightning
- The general docs are excellent: https://pytorch-lightning.readthedocs.io/
- The youtube channel: https://www.youtube.com/channel/UC8m-y0yAFJpX0hRvxH8wJVw  In particular,
  - https://www.youtube.com/playlist?list=PLaMu-SDt_RB5NUm67hU2pdE75j6KaIOv2
- Python Engineer youtube: https://www.youtube.com/watch?v=Hgg8Xy6IRig
  - Code is at https://github.com/python-engineer/pytorch-examples/tree/master/pytorch-lightning
- 

## Optimizing for Performance
A checklist of your code
- You should always `detach()` for any code that is not part of the computational graph
- If you are using the network without training it, make sure to call `net.eval()` and ensure it has a no_grad in one way or another (i.e. a `with torch.no_grad:`)
- You should basically never call `item()` inside of core differentiated algorithms.  Maybe in `detached` stuff.

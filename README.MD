#UPDATE TO RUN IN 2023
 1. Create a virtual environment with Python 3.6

 2. Navigate to the "bezier gan" directory
	cd path/to/bezier-gan-directory

 3. Create a new directory named "beziergan2"
	mkdir beziergan2

 4. Change your current directory to "beziergan2"
	cd beziergan2

 5. Create another virtual environment in "beziergan2" with Python 3.6
	python3.6 -m venv venv

 6. Navigate to the "venv/Scripts" directory
	cd venv\Scripts

 7. Upgrade pip to the latest version (user-specific)
	pip install --user --upgrade pip

 8. Activate the virtual environment
 On Windows
	.\Activate.ps1
 On other platforms, use the appropriate activation command

 9. Ensure you've chosen the correct Python kernel in your development environment (e.g., VSCode).

 10. Install TensorFlow version 1.15.5
	pip install tensorflow==1.15.5

 11. Install the NumPy library
	pip install numpy

 12. Install Protocol Buffers (protobuf) version 3.20.0
	pip install protobuf==3.20.0

 13. Install the Matplotlib library for data visualization
	pip install matplotlib

 14. Install the scikit-learn library for machine learning tasks
	pip install scikit-learn
	
 15. Run the GAN training script with the specified parameters
	python path/to/train_gan.py train 64 16




# Bézier-GAN

Experiment code associated with the paper: [Airfoil Design Parameterization and Optimization using Bézier Generative Adversarial Networks](https://arxiv.org/pdf/2006.12496.pdf)

![Alt text](/architecture.svg)

## License
This code is licensed under the MIT license. Feel free to use all or portions for your research or related projects so long as you provide the following citation information:

Chen, W., Chiu, K., & Fuge, M. D. (2020). Airfoil Design Parameterization and Optimization Using Bézier Generative Adversarial Networks. AIAA Journal, 58(11), 4723-4735.

    @article{chen2020airfoil,
	  title={Airfoil Design Parameterization and Optimization Using B{\'e}zier Generative Adversarial Networks},
	  author={Chen, Wei and Chiu, Kevin and Fuge, Mark D},
	  journal={AIAA Journal},
	  volume={58},
	  number={11},
	  pages={4723--4735},
	  year={2020},
	  publisher={American Institute of Aeronautics and Astronautics}
	}

## Required packages

- tensorflow<2.0.0
- pyDOE
- sklearn
- numpy
- matplotlib
- autograd

## Dataset

Our airfoil designs come from [UIUC airfoil coordinates database](http://m-selig.ae.illinois.edu/ads/coord_database.html).

The raw data contains variable number of points along airfoil curves. We created the training data by applying [B-spline interpolation](https://github.com/IDEALLab/airfoil-interpolation) on these designs and removed outlier designs.

## CFD solver

We use [XFOIL](https://web.mit.edu/drela/Public/web/xfoil/) as the CFD solver to evaluate the performance of the airfoil design.

## Usage

### Train/evaluate Bézier-GAN

Go to Bézier-GAN's directory:

```bash
cd beziergan
```

Train a Bézier-GAN or evaluate a trained Bézier-GAN:

```bash
python train_gan.py
```

positional arguments:
    
```
mode	train or evaluate
latent	latent dimension
noise	noise dimension
```

optional arguments:

```
-h, --help            	show this help message and exit
--model_id		model ID
--save_interval 	number of intervals for saving the trained model and plotting results
```

The trained model and synthesized shape plots will be saved under directory `beziergan/trained_gan/<latent>_<noise>/<model_id>`, where `<latent>`, `<noise>`, and `<model_id>` are latent dimension, noise dimension, and model ID specified in the above arguments.

### Run optimization

#### Bézier-GAN + Two Stage Optimization

```bash
python optimize_gan_bo_refine.py
```

positional arguments:
    
```
latent	latent dimension
noise	noise dimension
```

optional arguments:

```
--n_runs		number of experiment runs
--n_eval		number of evaluations per run
-h, --help            	show this help message and exit
```

#### Bézier-GAN + One Stage Optimization

```bash
python optimize_gan_bo.py
```

positional arguments:
    
```
latent	latent dimension
noise	noise dimension
```

optional arguments:

```
--n_runs		number of experiment runs
--n_eval		number of evaluations per run
-h, --help            	show this help message and exit
```

Optimization history and optimal airfoil shapes are saved under directory `results_opt`.

## Results

Randomly generated airfoils:

<img src=samples.svg width="640">

Optimization history:

<img src=opt_history_conventional.svg width="480">

Optimized airfoils:

<img src=opt_airfoils.svg width="960">





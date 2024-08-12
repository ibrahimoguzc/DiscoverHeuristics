This repository includes the codes for our study 'Heuristics Discovery Using Large Language Models'. The repository is composed of two main parts: heuristics discovery pipeline (heuristics_discovery) which includes my codes for the heuristic discovery pipeline and testing which includes the code for testing the discovered algorithms and also exact solution methods.

## Installation and Requirements

Please note that **the Python version must be larger or equal to Python 3.9**, or the '*ast*' package used in the implementations will fail to work. 

## Heuristics Discovery
The pipeline composes of two parts: an LLM agent and the main file. The LLM server should be loaded first from huggingface (you can also use an API-refer to https://github.com/RayZhhh/funsearch for implementation) and then the main file is run to initiate the pipeline. The requirements are given in 'requirements.txt'. huggingface-cli can be used to use any LLM of your choice. There are 3 main files:
	-main_edd.py
	-main_spt.py
	-main_mdd.py
They take different specifications and all of them are available under specification folder. Data used to train the functions can be changed from the main files. The logs are recorded to logs file, along with number of samples, all of the mentioned things can be manipulated within main file.  First the llm_server.py should be run and then one of the main files of your choice. It is crucial to have the same port that LLM is loaded in the main file. 

Project Structure

There are some independent directories in this project:

- `implementation` contains an implementation of the evolutionary algorithm, code manipulation routines, and a single-threaded implementation of the FunSearch pipeline. 
- `llm-server` contains the implementations of an LLM server that gets the prompt by monitoring requests from FunSearch and response to the inference results to the FunSearch algorithm. 

Files in `funsearch/implementation`

There are some files in `funsearch/implementation`. They are as follows:

- `code_manipulatoin.py` provides functions to modify the code in the specification.
- `config.py` includes configs of funsearch.
- `evaluator.py` trims the sample results from LLM, and evaluates the sampled functions.
- `evaluator_accelerate.py` accelerates the evaluation using the 'numba' library.
- `funsearch.py` implements funsearch pipeline. 
- `profile.py` records the score of the sampled functions.
- `programs_database.py` evolves the sampled functions.
- `sampler.py` sends prompts to LLM and gets results.


The instructions for running the pipeline with main_mdd.py are: 
#Load the LLM
cd heuristics_discovery/llm-server
python llm_server.py --port 3000 --quantization --path mistralai/Mixtral-8x7B-Instruct-v0.1 --gpu_ids 0 
#run the pipeline
python main_mdd.py



## Testing

The exact solutions for N=20 instances are generated using DP mainly, also MIP and MIP with VI approaches are used to compare. Relevant code is in the notebook 'exact_solutions.ipynb'.
The N = 100, 200 and 500 instances are taken from Shang et al (2017), refer to (https://github.com/vtkindt/1-dj-Sum-Tj) for their TTBM algorithm's code and data. Thanks to Dr. Vincent T'Kindt for sharing the material. The "heuristics_comparison.ipynb" is used to compare heuristics and optimal solutions.
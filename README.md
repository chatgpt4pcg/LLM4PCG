# The LLM4PCG Competition: Character-like Level Generation for Science Birds

![image](https://github.com/ZifanYE/ReadmeViewer/blob/main/LLM4PCG.png)

Welcome to the 2025 LLM4PCG Competition. Here you will be provided all the necessary information needed to participate in the competition. Please remember to read carefully and thoroughly before contacting us for any questions you might have. 

### What is the LLM4PCG Competition:
----
The LLM4PCG Competition continues the challenging and exciting spirit of the first and second Chatgpt4pcg competitions. In this edition, we not only challenge participants to come up with a prompt to construct stable Science Birds levels resembling uppercase English characters, but we also open up the possibility of incorporating more complex prompt engineering techniques. This time, we allow the submission of a program in which participants can build on top of our examples and packages, enabling the use of conditions and iterations in programming to develop their own advanced prompt engineering techniques, and potentially create new ones!

We welcome participants of all levels, whether you only modify a prompt in a provided example or come up with a complex logic through prompt engineering. All programs will be inspected for qualification, subject to the competition rules, and used to generate levels for each target English uppercase character. The generated levels are then tested for stability using our Science Birds Evaluator and checked for similarity to respective target characters using an upgraded Vision Transformer (ViT) classifier. This edition also introduces a new metric--diversity, making it more challenging. Now, not only do the prompts and/or prompt engineering techniques developed by participants need to generate stable and similar levels, but they also need to generate diverse levels.
### Quick Start:
----
1. Download LM Studio from [LM Studio](https://lmstudio.ai/).  
2. Download large language models from the "Search" page:  
To ensure fairness to the full，these **open-source models** are recommended to be used:
	+ `Q8_0` qwen2.5-32B [bartowski/Qwen2.5-32B-Instruct-GGUF](https://model.lmstudio.ai/download/bartowski/Qwen2.5-32B-Instruct-GGUF)  
	+ `Q8_0` phi-3-medium [ssmits/Phi-3-medium-128k-instruct-Q8_0-GGUF](https://model.lmstudio.ai/download/ssmits/Phi-3-medium-128k-instruct-Q8_0-GGUF)  
	+ `Q4_K_M` llama3.1-70B [bartowski/Meta-Llama-3.1-70B-Instruct-GGUF](https://model.lmstudio.ai/download/bartowski/Meta-Llama-3.1-70B-Instruct-GGUF)
	+ If your computer can't afford these models, you are welcome to use other open-source models. Finally we will evaluate the submitted prompts by these three models.  
3. Once the model is downloaded, navigate to the "Local Server" tab, select the model, and click "Start Server".  
Please view more details on [Prompt Engineering for Science Birds Level Generation and Beyond](https://chatgpt4pcg.github.io/tutorial)
4. You can start the tutorial code from [this github repository](https://github.com/chatgpt4pcg/tutorial-2024-notebook)  
5. We provide a few example programs implemented using various prompt engineering techniques. These examples are offered to assist you in getting started with the competition. You can utilize these examples as a foundation to develop your own advanced prompt engineering techniques. The examples are accessible in a GitHub repository, which you can find [here](https://github.com/chatgpt4pcg/pe-examples?tab=readme-ov-file) 
*(openai'key is needed to run the code for previous [ChatGPT4PCG 2 competition](https://chatgpt4pcg.github.io/))*

### Rules
---
#### General
1. Any form of cheating, as determined by the organizers, will result in automatic disqualification from the competition.  
2. Any intended attempts to harm the computing system used to conduct the evaluation process will result in automatic disqualification  
3. The organizers reserve the right to update the rules and details of the competition at any time. Any changes will be communicated through the changlog [here](https://chatgpt4pcg.github.io/changelog).  

#### Prompt Rules
1. The organizers reserve the right to update the rules and details of the competition at any time. Any changes will be communicated through our website.  
	1. A submitted program must implement the interface through the Python package provided by the competition to interact with your model via API and output final results in a specified format. Participants are not allowed to interact with your model via API through other methods.
	2. During each evaluation, we will use the latest version of the required competition's Python package available as of one week before the submission deadline
	3. Any tools needed for the implementation of prompt engineering techniques are the responsibility of the participants to provide to the organizers. We do not aim to provide any free or paid services required by your program. We do not guarantee the compatibility of additional tools required as a part of your program. Instructions on how to set up these tools must be provided by participants. In case you utilize paid services, such as gated APIs, proprietary software, or specialized databases, it is the participants' responsibility to provide any required information to run the said software and confirm with these providers about the licenses, terms, and agreements for use in this competition. Any parts of the software that could not be made public must be explicitly stated and informed to the organizer to be removed before being made publicly available. We recommend participants check the specifications of the evaluation computer to ensure compatibility beforehand.  
	4. The program must not modify responses from your model before writing them to files as final output for evaluation. We consider direct intervention to be cheating. Only the direct response from your model may be utilized as a final output.  
	5. Modification of the message history of your model in a way that is considered cheating, such as altering the message history with manually created content (i.e., hard-coding answers), is prohibited.  
	6. Modification of the token counter and timer used for the evaluation is prohibited.  
	7. In the event of an error during a trial, that trial will be treated as producing an empty response.  
	8. To ensure fairness, each program combined (source code, tools, databases, etc.) must be at most 1GB in total size including any data downloaded as a result of running the submitted program, and each trial will last only 120 seconds. The sampling temperature and random seed are always fixed at 1 and 42, respectively.  
	9. Automatic prompt optimization may be utilized, but its use during the evaluation is discouraged as it quickly consumes available token limits. Therefore, we suggest employing these techniques beforehand.  
2. Programs failing to follow the requirements in 1. will result in automatic disqualification.  
3. To ensure that code blocks can be extracted successfully from responses generated by the your model API, each output must include three backticks (```).  
	1. The code extraction script will only extract the content between the last pair of three backticks (```).
	2. The extracted code must not contain any loops. Any use of loops will be ignored, resulting in only one instance of the loop's content. The code should not use variables in the call of the `drop_block()` function, as this will result in an error and that response will be skipped for the rest of the evaluation process. To check the behavior of the code extractor, please refer to the [Resources](https://chatgpt4pcg.github.io/resources) page where you can find an online tool for this task.  
	3. If no code blocks are present or extracted code results in an empty string, the response will be skipped, and its score will be 0.  
4. All plugins and function callings are disabled during the evaluation process. 
5. The final response from your program must explicitly include a series of `drop_block()`, which will be executed in that order by our tool to generate a character-like structure in a Science Birds level.  
6. The definition of the `drop_block()` function is as follows: 
	1. It drops a block vertically drop a block from the top and center it at a specific slot, denoted by `x_position`.  
	2. This function works on the following settings:  
		1. A structure is situated on a 2D grid with a width (`W`) of 20 columns and a height (`H`) of 16 rows. The grid consists of 320 cells, each of equal size.  
		2. Coordinates `(x, y)` are used to represent the positions in the grid, where `x` and `y` show the horizontal and vertical indices of cells, respectively. For example, `(0, 0)` denotes the bottom-left corner cell of the grid, and `(W-1, H-1)` is the top-right corner cell.  
		3. A cell on the grid has a size of 1x1. Each cell has unique `(x, y)` coordinates associated with it.  
	3. This function accepts two parameters:  
		1. `block_type`: a value that indicates the type of block to be placed. The possible values are`b11`, `b13`, and `b31`. An invalid block type will result in an error.  
			1. `b11` denotes a square block whose size is 1x1.  
			![image](https://chatgpt4pcg.github.io/images/nextImageExportOptimizer/b11-opt-48.WEBP)
			2. `b13` denotes a column block whose size is 1x3.  
			![image](https://chatgpt4pcg.github.io/images/nextImageExportOptimizer/b13-opt-48.WEBP)
			3. `b31` denotes a row block whose size is 3x1.  
			![image](https://chatgpt4pcg.github.io/images/nextImageExportOptimizer/b31-opt-256.WEBP)
		2. `x_position`: a horizontal index of a grid cell, where `0` represents the leftmost column of the grid, and `W-1` represents the rightmost column of the grid. The `x_position` parameter indicates the center pivot point of the block being placed. For example, if `b31` is the only block in the level and is placed at `x_position=4`, it will occupy cells `(3, 0)`, `(4, 0)`, and `(5, 0)`. An invalid position, like a position where a block of interest intrudes on the grid boundary, will result in an error.  



### What To Submit:
---
#### Submission Guideline:

Before submitting, please ensure that your program follows our guidelines by checking the Rules. It is particularly important that the `drop_block()` function used in your program is defined in the same way as our rules. If not, your results may be unexpected.  
Your submission can be made using the following form: (coming soon)

    # Team Name
    
    ## Team Members
    
    List the names of the members of this team.
    
    ## Overview
    
    Briefly describe your approach.
    
    ## Instructions
    
    Describe what are the necessary environments or specific steps to run your program after unzipping the file.
    
    ## How to Run
    
    Include detailed instructions on how to run your program. This may include commands, configurations, or specific steps.
    
    ## Dependencies
    
    List all dependencies required to run your program. This may include libraries, frameworks, or specific software versions.
    
 
To participate, you must submit your prompt according to our guidelines. We will then generate a number of samples, each of which will undergo rigorous testing for stability, similarity, and diversity. Stability will be evaluated by loading the level in Science Birds and examining the ratio of unmoved blocks after 10 seconds of the initialization. The similarity of each generated level to its corresponding English character will be determined using an open-source ViT-based classifier model. The stability testing system and the instructions to use the classifier model, as well as all the relevant tools, will be provided. The newly introduced diversity is assessed by averaging the distances of unordered pairs of output vectors from the ViT classifier across trials, all pertaining to the same target character and prompt.

We hope that this edition will be more exciting and contribute to collective learning and discovery in the world of prompt engineering through this game competition!

> __To obtain more information about the competition, please do not hesitate to visit our previous competition website [here](https://chatgpt4pcg.github.io/), where you can find detailed information and updates regarding the event.__  
#### Submission Rules
1. If a team submits multiple entries during a stage, midterm or final, we will consider the most recent submission as that team's final submission.  
2. Submissions received after the deadline will not be considered for the evaluation process.  
3. By submitting, you accept all rules and agree that all submitted prompts and programs will be made public.  
#### Result Announcement
All participating teams will receive email notifications of their results using the email addresses provided in the submission email. The winner will also be announced on our website.
### How To Evaluate:
---
#### Evaluation
The submitted prompts will undergo an evaluation process that involves subjecting them to 10 trials for each of the 26 uppercase letters of the English alphabet (A-Z). The levels generated for each character will be evaluated based on their similarity, stability, and diversity, and scored using the criteria outlined in the scoring policy given below. The entire evaluation process will be conducted using automated scripts and programs.  
Please note that the evaluation process will be conducted twice, at midterm and final stages. The number of trials and characters in the evaluation set may be adjusted based on the number of teams.
#### Evaluation Set
All 26 alphabetical uppercase characters.

A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
#### Scoring Policy
Please click [here](https://chatgpt4pcg.github.io/evaluation#scoring-policy) for Score Policy information.
### Evaluation Tools
1. We will conduct the final evaluation on these 3 models:
	- qwen2.5-32B
	- phi-3-medium
	- llama3.1-70B

 	While participants are free to explore other models during their research phase, our final assessment will be a comprehensive evaluation of submitted projects based on these three models.

2. [Science Birds Evaluator](https://github.com/chatgpt4pcg/modified-science-birds) with features to:
   - Automatically assess the stability.
   - Automatically export images using black-textured blocks on a white background for similarity testing.

3. [vit-base-uppercase-english-characters](https://huggingface.co/pittawat/vit-base-uppercase-english-characters).

4. Automation scripts available on our [Resources](/resources) page.
#### Evaluation Environment for Response Generation Stage
Software:  
	- OS: macOS Sonoma Version 14.5  
	- Python: 3.11.xx  
	- Unity: 2019.4.40f1 
	- [Science Birds Evaluator  ](https://github.com/chatgpt4pcg/modified-science-birds)  
	- [Our automation scripts](https://chatgpt4pcg.github.io/resources)  
	 
Hardware:  
	- Chip: Apple M2 Ultra
	- RAM: 128 GB

#### Evaluation Process
1. We manually inspect each submitted program for a potential violation of the rules.  
2. Submitted PE will be evaluated on all three models (average score)
3. Better PE performs well on all models
4. We will test generalizable of prompt engineering
3. The [code extraction script](https://github.com/chatgpt4pcg/code-extraction-script) will load each response and produce a new file containing only a series of `drop_block()` commands.   
4. The [text-to-xml conversion script](https://github.com/chatgpt4pcg/text-to-xml-converter-script) will load each code file and convert it into a Science Birds level description XML file.
5. Next, [Science Birds Evaluator](https://github.com/chatgpt4pcg/modified-science-birds) will individually load all levels to assess their stability and capture their images. The results of stability will be recorded, and for each level an image of the structure with black-textured blocks on a white background will be produced by the program.  
6. The [similarity checking script](https://github.com/chatgpt4pcg/similarity-checking-script) will load each image and pass it through an open source-model called [vit-base-uppercase-english-characters](https://huggingface.co/pittawat/vit-base-uppercase-english-characters). It will then record the similarity result.  
7. The [diversity checking script](https://github.com/chatgpt4pcg/diversity-checking-script) assesses the diversity of the levels by averaging the cosine distance of non-duplicated all-pairs of outputs from softmax for each level across trial of the same target character as described in the [Evaluation](https://chatgpt4pcg.github.io/evaluation).  
8. The [scoring and ranking script](https://github.com/chatgpt4pcg/scoring-and-ranking-script) will load all stability, similarity, and diversity results and produce the final rank and score result for all teams according to the scoring policy.
9. Finally, we will calculate the sum of scores for all three models.Evaluation process for results from each model is same as this year competition.



### Prizes:
---
In this year, we have a total of 1000 USD in prizes to be awarded to:

- 🥇 **1st Place** - 500 USD
- 🥈 **2nd Place** - 300 USD
- 🥉 **3rd Place** - 200 USD

The prize is sponsored by the IEEE CIS Education Competition Subcommittee. The organizers would like to express their gratitude to the IEEE CIS Education Competition Subcommittee for their generous support.  
If you are the winner and eligible to receive the prize, you agree that your email address associated with the submission will be shared with the IEEE CIS Education Competition Subcommittee.
### Organizers:
---
1. Yi Xia, Graduate School of Information Science and Engineering, Ritsumeikan University
2. Pratch Suntichaikul, Graduate School of Information Science and Engineering, Ritsumeikan University
3. Zifan Ye, Graduate School of Information Science and Engineering, Ritsumeikan University
4. Febri Abdullah, Graduate School of Information Science and Engineering, Ritsumeikan University
5. Mury F. Dewantoro, Graduate School of Information Science and Engineering, Ritsumeikan University
6. Ruck Thawonmas, College of Information Science and Engineering, Ritsumeikan University
7. Julian Togelius, NYU Tandon School of Engineering, New York University
8. Jochen Renz, School of Computing, The Australian National University


### Submission deadline:
---

### Contact Us:
---
If you have any questions, please contact us at this email address.  
Email address: <chatgpt4pcg@gmail.com>

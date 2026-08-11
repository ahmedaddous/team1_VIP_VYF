# Ancient Greek Embeddings Subteam
Welcome! Our subteam is mainly responsible with training good word (and sentence) embeddings of Ancient Greek text. Each 
subfolder in this repository has a purpose which is explained in yet another README found within it. If you're lost reading something here, chances are that having a look at the READMEs in the appropriate subfolders will help! We don't work with most of 
these subfolders anymore, but we keep them for the sake of documentation.

# Previous Progress
- First, we created the corpus; we then trained a number of FastText models and evaluated the embeddings through cosine 
similarity. (Go to `corpus_files/README.md` `training_files/README.md` for more!)
- We then implemented something known as _Bilingual Lexicon Induction_ and tested it out. (Go to `BLI_files/README.md` for more!) 
- Finally, we moved on from FastText models, and have most recently trained a BERT-based model from scratch. (Go to `greek_bert/README.md` for more!)

Here's a [link](https://...) to the final progress presentation we gave during the Spring 2026 semester. 

# Next Steps
- [ ] Tweaking the hyperparameters of the BERT-based model 
- [ ] Moving on to coming up with good sentence embeddings rather than focusing on word embeddings only. 

# Using PACE-ICE
A lot of computation is needed when it comes to training the models we do. Luckily, as part of the VIP, you all have access to
the PACE-ICE computing cluster. There are a decent amount of [computation options](https://gatech.service-now.com/home?id=kb_article_view&sysparm_article=KB0042095) provided to you (scroll down to "ICE Compute Nodes"), so it's worth having an understanding of PACE-ICE!

To log into PACE-ICE, you first need to be connected to the campus VPN or Wi-Fi network. (Follow [this guide](https://gatech.service-now.com/home?id=kb_article_view&sysparm_article=KB0042139) to set that up.)
Then, once you connected through the VPN, run the following command in your terminal:

````bash
ssh gtusername@login-ice.pace.gatech.edu  
````

Then, enter your password and you should be granted access. Congratulations, you're on PACE-ICE! Specifically, you're on a
login node. You shouldn't be running any heavy scripts here; to learn how to submit scripts, I'd highly recommend the  [Intro-To-Pace-ICE](https://github.com/guru-desh/Intro-To-PACE-ICE) guide, and, of course, the [official guide](https://gatech.service-now.com/home?id=kb_article_view&sysparm_article=KB0042102).


# Recommendations
As you work through, you'll have to train models and keep track of their performance. My recommendation is to 
__store everything on the shared folder of your subteam__. Ideally, you have a folder called `models` in there, which consists
of subfolders, each containing a model and its performance. While this means you won't be able to keep the model on GitHub, it
ensures that you aren't polluting your own space. In addition, you can run out of space in your home folder, so you won't be able to do much anyways. Finally, it's a way to keep track of how each combination of hyperparameters affects performance.  

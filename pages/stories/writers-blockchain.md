---
title: Writer's Blockchain
week: 26
slug: writers-blockchain
date: "2022-07-30"
episode_url: 'https://whatrocks.github.io/f52a/26.mp3'
episode_duration: '872'
episode_length: '17445533'
episode_summary: Week 26
episode_explicit: 'no'
---

<audio controls="controls">
  <source type="audio/mp3" src="https://whatrocks.github.io/f52a/26.mp3"></source>
</audio>

"Halfway through," said Charlie, staring at the largely blank Markdown file for week 26 of his 52 week short story writing challenge. "I wonder if I've written a good one yet?"

He thought about checking his Cloudflare web analytics, but stopped himself. Nothing good could be found there. Besides, he was supposed to be writing. He'd gotten a bit of traction with a few sci-fi-ish stories on Hacker News, which gave him a decent bump in page views -- *readers*, he corrected himself -- but nothing to write home about. Not yet, at least. Ray Bradbury did say it might take until #52 for a good one to pop out.

Instead of writing anything, anything at all, Charlie got up to re-microwave his third cup of coffee of the day for the second time. Something was bugging him -- something he'd seen on the orange site.

> DALL-E 2.

A new AI model that could produce truly creative, wondrous works of art with a simple prompt of text as input. A phrase, a song lyric, a fever dream, whatever -- just type it in and the helpful AI will helpfully spit back something helpful and probably completely earth-shatteringly stunning.

Charlie tried not to feel concerned about DALL-E and what it meant. Charlie was a believer in technology, after all. Moreover, he was a day-dreamer of technology, forever lost in books of the near-future and far-future, with its tricorders and space elevators and solarsails. Charlie knew by heart that whenever something new comes along, people get scared and worried about their livelihoods. It just so happened that technology was now coming for the creative class: DALL-E for art, GPT-3 for writing, and even GitHub Copilot for coding. These AI harbingers were only the beginning of what would come next, mere trilobytes of AGI.

Charlie tripped on his laptop's charging cable walking back to his desk and spilled coffee on his new grey Boba Fett t-shirt, right on the green bounty hunter's dented helmet -- which Charlie now knew was a Mandalorian helmet thanks to the limited series.

He Googled *remove coffee stain from t-shirt* on his phone. After some laundry urgent care, Charlie came back to his desk wearing a hoodie, which only meant one thing: Charlie the writer had become Charlie the coder.

"If you can't beat 'em..." said Charlie, in a terrible John Wayne accent. Then, in an even worse Michael Caine: "In the face of new technology, one must elevate their work or perish. No longer do we need toil with oils and watercolors as artists. We must instead become as magician's apprentices."

Then Charlie felt embarrassed for himself. But he still got to work.

His first idea was to try out GPT-3 for this week's story. Maybe this AI wizard-godhead could write his next story for him, and Charlie could just do some sit-ups and pushups instead (he was always feeling guilty that he wasn't currently doing sit-ups and pushups at any given moment. His dad did say that someone else was always outside shooting free throws when Charlie was inside playing Nintendo 64. But did that person have all 120 stars and meet Yoshi on the roof of Peach's castle? Charlie didn't think so.) But then Charlie discovered that he didn't have access to GPT-3. Or DALL-E2 for that matter. It seems that only a select few had been granted the skeleton keys to these mysterious beasts.

Charlie tapped his Bluetooth keyboard without actually pressing the keys, like he was feverishly typing something.

"You know," said Charlie to no one in particular. "After 25 weeks of this short story business, I've got enough text of my own that maybe I could train my own AI language model... something that could write *exactly* like me."

He kept on fake typing and talking to himself.

"I know can't make it... like, actually, good, like GPT-3 or anything. But what about something simpler... a Markov chain!"

Charlie had played with Markov chains before. In fact, he'd written a toy commencement speech generator using Markov chains, trained on he considered to be the best graduation speeches in history -- connecting the dots in reverse and whatnot. He could do the same thing here, but with his stories as input.

"Okay, let's do it. First thing, I need to grab all of my stories and dump them into a fresh directory. I'll make the directory first"

```bash
$ cd
$ mkdir charlie-ai
$ cd charlie-ai
```

"Okay, I know I'll need a Python file for writing my Markov chain code, so let's add that as a placeholder for now."

```bash
$ touch markov.py
```

"And a fresh new folder for my stories."

```bash
$ mkdir stories
```

"Cool. Now I need to copy over all my stories to this new *stories* folder. Good thing I read that old Unix book recently." Charlie looked around for a rubber duck - something to talk to - and he settled on a small blue poison dart frog figurine that he'd bought in Vineland, New Jersey during one perfect summer week with his cousins.

```bash
$ cp ../fahrenheit-52/pages/stories/*.md stories/
```

Charlie hummed. "Did it work, little frog? To check, I'll list the directory and then pipe it to the word count command and count the lines. Gotta love those Unix pipes!"

```bash
$ ls stories | wc -l
26
```

"Awesome. But why is it 26 stories and not 25? Oh, wait. That does make sense. I primed the pump with a zeroth story at the beginning of the year, so there's 26 right now. Cool. Oh! I should probably remove all that frontmatter at the beginning of every story. Don't want that stuff cluttering up my AI's brain."

Charlie confirmed the frontmatter's presence with the *head* command, listing the first 20 lines of a random story:

```bash
$ head -5 stories/plastic-man-on-the-moon.md
---
title: Plastic Man on the Moon
week: 19
slug: plastic-man-on-the-moon
date: "2022-05-09"
episode_url: 'https://whatrocks.github.io/f52a/19.mp3'
episode_duration: '272'
episode_length: '5445402'
episode_summary: Week 19
episode_explicit: 'yes'
---

<audio controls="controls">
  <source type="audio/mp3" src="https://whatrocks.github.io/f52a/19.mp3"></source>
</audio>

**APOLLO 11 LOG : 20220509-1045**

Neil Armstrong's a liar.
```

"Ugh. Gross. Let's get rid of that stuff."

To clarify, at the beginning of every Markdown file was something called frontmatter - which was basic metadata about the story, including its title, URL slug, and publishing date. The frontmatter also included some stuff used to generate Fahrenheit 52's podcast feed - a neat feature that Charlie had added to his friend Ben's static site generator.

"Let me Google this... *how to remove first X lines of text file*. No, that wasn't right. I want a one-liner here. Let me try another one: *Delete first n lines from all files in directory*. Boom! Now we're talking. The mysterious and powerful *sed* command."

Charlie manually counted out the number of lines to remove (16), then copy-pasted the Unix command from the Internet, adjusting it slightly.


```bash
$ sed -i '' -n '16,$p' stories/*.md
```

"Did it work?"

```bash
$ head -5 stories/plastic-man-on-the-moon.md

**APOLLO 11 LOG : 20220509-1045**

Neil Armstrong's a liar.
```

"Perfect! I should really learn how to use *sed* and *awk* one of these days." Something else struck him. "Hey frog -- maybe Googling - and being good at Googling - is like... an analogy for how people will interact with AI tools like DALL-E. Sure, everyone can Google. But, c'mon... some people, like me, are just better at it. Same thing for these DALL-E prompts, right?"

The frog said nothing. 

"Well, it's not like I have access to DALL-E anyway. Let's keep moving. Time to dive into our Python file."

```bash
$ vim markov.py
```

"Welp, we've found ourselves in front of another blank page, frog. I know I need a few things, though. One, I should try to see what that Markov library I used was. No time to write our own, but that would be fun. Also, I know I'm going to need to loop through all my stories and ingest them into the Markov chain library. Why I don't I do that bit first?"

```python
filename = "stories/plastic-man-on-the-moon.md"
with open(filename) as f:
    text = f.read()
    print(text)
```

"That's obviously terrible, but let's just see if that even worked."

```bash
$ python markov.py
```

Charlie's story about a plastic action figure left behind on the Moon by Neil Armstrong printed to the terminal.

"Great. Lemme see if I can dig up my old code and see what that library was..."

Charlie searched on GitHub in his public repositories and found his *markov-commencement-speech* repo. The Python library in question was called *markovify*.

"Okay, so I don't remember how to use this library, frog. I guess I could look up its documentation. But that's too much work. Actually, what if I tried GitHub Copilot for this?"

He fiddled with his vim settings to reenable Copilot and then deleted everything his current markov.py file. Charlie opened it up again and typed out a few lines, the second one incomplete:

```python
import markovify
with open(
```

Just as Charlie tapped the open parenthesis, Copilot suggested this:

```python
with open("corpus.txt") as f:
  text = f.read()
```

"Woah," said Charlie, channeling his best Neo. Then he typed Return and wrote "markovify" on the next line.

```python
with open("corpus.txt") as f:
  text = f.read()
  markovify
```

Copilot suggested this:


```python
with open("corpus.txt") as f:
  text = f.read()
  markovify_model = markovify.Text(text, state_size=2)
```

"Super cool. I'm not sure why I stopped using Copilot. I know they're charging for it now, so it must be working for a lot of people. But I think I have an even easier approach."

Charlie went back to his Github repo for the commencement speech thing, copy-pasted the code from his Jupyter notebook file into his "markov.py" Python file, and made a few tweaks, here and there, like a good software engineer does when they copy-paste stuff.

```python
import os
import markovify

STORIES_PATH = 'stories/'

story_dict = {}
for story_file in os.listdir(STORIES_PATH):
    with open(f'{STORIES_PATH}{story_file}') as story:
        contents = story.read()
        # Create a Markov model for each story in our dataset
        model = markovify.Text(contents)
        story_dict[story_file] = model

models = list(story_dict.values())
print(f'There are {len(models)} stories in our dataset.')

# Combine the Markov models
model_combination = markovify.combine(models)

# Generate 5 sentences
for i in range(5):
    print(f'{i}: {model_combination.make_sentence()}\n')
```

"Okay, let's give it a go."

```bash
$ python3 markov.py
Traceback (most recent call last):
  File "/Users/ch/projects/charlie-ai/markov.py", line 2, in <module>
    import markovify
ModuleNotFoundError: No module named 'markovify'
```

"Ah, right. I need to install the *markovify* library in this project. What the heck is the virtualenv command again?" He tried reverse-i-searching-or-whatever for "virtualenv", but no dice -- it had been a while since Charlie touched Python stuff -- so he just Googled again to find the incantations:

```bash
$ python3 -m venv .charlie-ai
$ source .charlie-ai/bin/activate
(charlie-ai) $ pip install markovify
(charlie-ai) $ python markov.py
There are 26 stories in our dataset.
0: Or how it would be perfect.

1: One of those old skeleton keys with two legs was sticking out from under the bushes.

2: They found remnants of an empty cicada husk -- the other two Space Force officers attempted to hold both Daniel and found a large tree branch and used it as a crown.

3: Callan imagined his father done to him?

4: You had to wrangle with the best of them.
```

Charlie smiled.

"Cool! Lemme try again..."

```bash
(.charlie-ai) ch charlie-ai $ python markov.py
There are 26 stories in our dataset.
0: He didn't even know, and also there was much of a frontier militia.

1: / .-. ..- / --- .--. / ..

2: I let go of Maria's wrist and she navigated into a long sip of his glow.

3: You could also just decline the next day and pestered his aunt about when they'd be heading to the core stone models.

4: I swim in the scruff of Bugg's neck.

```

"Right, I forgot about that Morse code story. Whoops. Probably could just remove that story from this Markov thing." 

Then Charlie's attention drifted and without even consciously thinking about it, he found himself on Hacker News. One of the top stories was from someone who quote "stripped" down DALL-E Mini (whatever that was) and shared it on GitHub. Even better, they'd included a Google Colab link, which was basically Google's hosted Jupyter Notebook environment. Which meant that Charlie could easily try out this DALL-E Mini thing - no waiting list needed.

"I'm going to see what it comes up with for my *Plastic Man on the Moon Story*, froggie!"

> action figure marooned on the moon

![Action figure 1](/story-images/moon.png)

"Cool! That sorta looks like claymation, in a good way. Let me try tweaking it a bit."

> plastic action figure left behind on the moon by neil armstrong

![Action figure 2](/story-images/moon2.png)

"Hmm, kinda worse. Let's try *The Young Adventures of Warren and Chuck* story," said Charlie. He tapped in a new prompt to the Jupyter notebook cell.

> young warren buffet as indiana jones

![Warren 1](/story-images/buffet.png)

"That's not bad! Just for good measure, lemme try another."

> warren buffet as adventurer indiana jones

![Warren 2](/story-images/buffet2.png)

Charlie screamed. "No, no, no... must adjust."

> young man warren buffet as adventurer indiana jones

![Warren 3](/story-images/buffet3.png)

"Phew, back to the safe and sound uncanny valley. Looks like a Goldeneye 64 character. Let's move on, frog. I want to try my *Voyager III* story."

> voyager space probe above backyard

![Voyager 1](/story-images/voyager.png)

"Meh, maybe I need more detail?"

> voyager space ship hovering over basketball court

![Voyager 2](/story-images/voyager2.png)

"Weird, but cool. Last one - I'll try *Grace and the Green Night*."

> man with glow in the dark green skeleton

![Skeleton 1](/story-images/skeleton.png)

"Good lord. I'm going to see that in my nightmares, aren't I, frog? One more try."

> person who has green skeleton

![Skeleton 2](/story-images/skeleton2.png)

"I agree, frog. We need to stop doing this or we're never going to actually write this week's story. Hopefully the real DALL-E 2 is less scary than this Mini one. Still, maybe I should figure out how to sell these as NFTs first? Cause that could be fun and interesting, and then I'd be able to..."

Just then, Charlie got an email from OpenAI.

He'd been granted access to GPT-3. Charlie completed the account registration process and opened up the Playground. He glanced at the tree frog, feeling guilty for some reason. He tapped in his prompt.

> Write an extended story about a writer who spends more time playing with AI tools like GPT-3 and DALL-E 2 instead of actually doing any writing.

GPT-3 thought for a moment. Then it started writing:

> I used to be a writer. I spent hours at my desk, crafting stories and essays that I hoped would resonate with readers. But these days, I find myself spending more time playing with AI tools like GPT-3 and DALL-E 2. I'm not sure what it is that draws me to these tools, but I can't seem to help myself.

> I start my days by firing up GPT-3 and asking it to tell me a story. I never know what I'm going to get, but I always find myself fascinated by the results. Sometimes the stories are nonsensical, but other times they're eerily accurate predictions of the future. I can't help but wonder if there's something to these stories that I'm not seeing.

> After I've had my fill of GPT-3, I move on to DALL-E 2. This tool is even more fun, in my opinion. With DALL-E 2, I can feed it images and it will generate stories based on those images. Again, the results are often bizarre, but sometimes they're so spot-on that it's scary.

> I used to spend my days writing, but now it feels like I'm just playing around with these AI tools. I'm not sure what's come over me, but I can't seem to help myself. I'm not sure what the future holds, but I have a feeling that these AI tools are going to play a big role in it.*

Charlie's feet tingled like they'd fallen asleep. He thought about that John Adams quote about his children, and then Googled it, because he didn't have it memorized and wanted to see the full thing:

> "I must study politics and war that my sons may have liberty to study mathematics and philosophy. My sons ought to study mathematics and philosophy, geography, natural history, naval architecture, navigation, commerce and agriculture in order to give their children a right to study painting, poetry, music, architecture, statuary, tapestry, and porcelain."

Staring his laptop screen, Charlie wondered what his children would study. Hopefully, they'd be explorers.
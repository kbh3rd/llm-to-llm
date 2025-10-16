## LLM-to-LLM Conversation Orchestrator

This page interacts with the APIs on two
[llama.cpp](https://github.com/ggml-org/llama.cpp) Large Language Model
servers, *i.e.*, chatbots, orchestrating an automatic conversation between
them. The servers can be on the same machine, on two separate machines,
and can even be the same single server. If not the same server, the two
instances can be running with different models.

Two separate conversation histories are maintained, one for each side
of the conversation where one bot's output is presented as input to the
other bot. Separate system prompts define the personality and behavior
of each bot. The default prompts define one bot as a user, and the other
bot as the AI assistant. Have fun playing with these system prompts to
get different sorts of interactions and personalities.

The conversation is kicked off by an initial prompt entered by the you,
the user. It runs for a certain number of interactions configurable on the
web page. Either of the instances can be chosen to take the initial prompt
and start off the conversation; be sure the system prompts accomodate
whichever goes first and which initially responds. Conversations can
be continued after they stop, and you can change the length of the
continuation.

Needless to say, the quality and depth of the conversations that you
get are largely dictated by the selection of language models used on
the servers.

### To do

Is any software project ever really done? (*Hint: No.*) Here are some of the most obviouis
enhancements and fixes that suggest themselves.

1. The URLs for both sides of the conversation could be entered by the user, with sane default
provided by the page source, instead of simply selecting between the two hard-coded URLs. This
could be useful in experimental environments with more than two chatbots available with APIs.
*Effort: Easy*
2. Better CSS layout and colors.
*Effort: Easy*
3. Interpret and properly render mark down formatting in the bots' responses.
*Effort: Easy to moderate*
4. Hide/Reveal the configuration elements of the page with a mouse click or tap to clean up
the page.
*Effort: Sorta Easy*
5. Let the user *optionally* enter the prompt with which to continue the conversation.
*Effort: Harder*
6. Let the user edit any of the intermediate responses before continuing the conversation to
redefine where it's going without starting from scratch.
*Effort: Hard*
7. Individual user-selectable settings for temperature and other API parameters would be nice.
Item #4 above would be a good prerequisite to avoid having the page get to large and ugly.
*Effort: Easy*
8. Support for API authentication. I'm using local firewalled instances of llama.cpp without an API key,
so I'm not sure how that's implemented. But it's probably *Effort: Easy*
9. Many others.
*Effort: Yeah*

### Implementation 

To make this work you need to edit the web page and customize the API URLs
in ```serverURL1``` and ```serverURL2```. They can be the same, and indeed
there may be little to no advantage to running two instances if they're
both of equal capability running the same model.

The code uses the ```/completion``` API endpoint. While implemented with
and for llama.cpp servers, other LLM implementations with an *identical*
API would work too, of course. The code requires that the servers/models support the specific grammar used. Example snippet:
```
<|begin_of_text|><|start_header_id|>system<|end_header_id>
system prompt...
<|eot_id>
<|start_header_id|>user<|end_header_id>
user prompt...
<|eot_id>
```
This format is typical for APIs that handle conversational state,
where the model processes the entire history to generate contextually
relevant responses.

It should not be surprising that AI was used in the process of crafting
an AI-focused application. [Grok](x.ai) was used to create the page. It
took several rounds of human debugging and additional prompting to get it
into a useable form. Several modifications to the AI-generated code were
done solely by hand. But the core structure is that which was received
from Grok.

Realistically, if there's one language that you're going to use AI for
help coding, it's gonna be Javascript, right?

Are there other implementations of essentially the same thing out
there? Frankly, I'd be surprised if there weren't. But what's the fun
in that?

----

$Revision: 1.5 $
$Locker:  $

*Yeah, I use RCS locally. So sue me.*

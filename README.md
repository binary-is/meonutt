# About Meonutt

Meonutt is an experimental project for advanced message handling in Neomutt.

The name wasn't picked specifically to confuse you, it was just a random idea. It can be changed if it's intolerable.

Please make sure to read the important caveats! They regard security!

## Status

This is currently a personal experiment and not intended for mainstream adoption. Feel absolutely free to copy the ideas presented here and do whatever you want with them. It currently assumes an independent passion for Neomutt.

A separate [`TODO.md`](TODO.md) document is maintained for now, which includes itemst like improving documentation and making it easier to set up and configure.

# The problem

Once you've gone through the trouble of setting up Neomutt and configuring it to your liking, it's pretty awesome, except at one thing: actually viewing email.

Terminal mail clients are sort of forced to look at HTML messages, PDF attachments and such as anomalies, because they cannot reliably display web pages or images, as these things are contrary to the paradigm of the terminal.

But they are not anomalies, they are the norm, unfortunate as that reality may be.

Three problems in particular are more-or-less impossible to solve elegantly using the terminal:

1. Displaying complex HTML or HTML with images.

2. Displaying PDFs.

3. Receiving attachments to the local computer is cumbersome when using Neomutt on a remote server through SSH.

# The solution

Meonutt takes messages piped from Neomutt (through MIME-type binding) and serves them through a local web server. The
local URL is then copied to the clipboard.

Let's imagine an email message that has only HTML with a bunch of important images, and a PDF attachment. Then the workflow is as such:

1. The user opens the message in Neomutt, seeing that it has two parts, HTML and PDF.

2. The user presses `Enter` on the HTML part, which pipes the message to Meonutt.

3. Meonutt opens a local HTTP server that serves the HTML, by default at [http://localhost:9000](http://localhost:9000).

3. Meonutt also **copies that URL** to the clipboard.

4. The user opens a browser and pastes the the URL into a browser.

5. The user enjoys the browser content while being tracked through remote images and hacked through JavaScript.

# IMPORTANT CAVEATS!

- There is currently no protection against remote servers detecting when you've opened the message. Such protections are
commonplace in modern email clients, but it has still not been implemented in Meonutt. It must be done, however.

- No filtering of JavaScript takes place. Any JavaScript that is in the HTML will get run in the browser on your
localhost.

Both of these should be fixed.

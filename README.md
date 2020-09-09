# Creating Icons For the Pokédex: An Application of Generative Adversarial Networks
The included Jupyter Notebook contains a neural network which trains on and generates images like those from the `Icons/` or `Artwork/` directory, both of which contain web-scraped Pokémon icons. Note that adjustments must be made for the neural network to train using the help of a GPU (which is highly recommended), as the original was trained within a VirtualBox without access to a GPU.

Below is a visualization demonstrating the quality of the generated images (right) versus the original, authentic images (left). 

![](https://scontent-lax3-1.xx.fbcdn.net/v/t1.0-9/118866343_117093613453158_111236074245876504_n.jpg?_nc_cat=100&_nc_sid=8024bb&_nc_ohc=23A2ffxJ97QAX-F3xbG&_nc_oc=AQkA4ZQ3yOXFsUHy3iUOwIeOiRhWfIAr0bJKS1tQzd8CYzWM3htZcKoC9-kkjUkZNcQ&_nc_ht=scontent-lax3-1.xx&oh=c423b0c8c74d7a76ca49d1de50c75af0&oe=5F7E446E)

Also included are two helper scripts within either aforementioned directory (`Icons/` and `Artwork/`) which locally download images given the URL. The `Icons/` directory contains URLs taken from the Pokédex `pandas` DataFrame made [here](https://github.com/niminuko/poke-webscraping); `Artwork/` contains URLs taken from the form `https://www.serebii.net/swordshield/pokemon/{poke_id}.png`, where `{poke_id}` is the associated ID for a given Pokédex from the Pokédex `pandas` DataFrame.

### Using Different Training Images
The key to easily gathering images together for training the GAN is to find an image URL (or family of image URLs) with a predictable format. For example, the `Artwork/` directory relies on a helper script to iterate over different values of {poke_id} in the `serebii` URL above. 

If, say, it was desirable to create a directory `Yugi/` for Yu-Gi-Oh! images then a URL such as `https://www.yugioh.com/cards?page={page_number}` would be used, with `{page_number}` ranging from 1 to 143. The helper script from either existing directory would be copied and made to iterate over the new URLs. The images would then be locally downloaded to the newly created directory; however, the images must be moved to a subfolder titled `1` in order to be read with a `torchvision ImageFolder`. A straightforward solution is to simply `mkdir ~/Pokemon/Yugi/1; mv *.png $_`.

Note: before running the helper script to download all the images, be sure to back out of the directory on the sidebar. This prevents Jupyter from trying to display thousands of newly created images in the sidebar at once, which typically causes Jupyter to become unresponsive.
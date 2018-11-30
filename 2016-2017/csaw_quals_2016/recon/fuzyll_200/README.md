<span class="c9">Fuzyll Writeup</span>

<span class="c1"></span>

<span class="c1">So for the beginning of this challenge, you are given the url:</span>

<span class="c5">[http://fuzyll.com/files/csaw2016/start](https://www.google.com/url?q=http://fuzyll.com/files/csaw2016/start&sa=D&ust=1543614497360000)</span><span class="c1"> </span>

<span class="c1"></span>

<span class="c1">And you get the following message:</span>

<span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 648.50px; height: 86.00px;">![](images/image7.png)</span>

<span class="c1">So what kind of colorblindness does Fuzyll have? Idk. But Wikipedia knows all the different kinds.</span>

<span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 397.00px; height: 251.00px;">![](images/image8.png)</span>

<span class="c1">Yeah, not many types. The kind Fuzyll has is deuteranomaly so just replace the “start” in the original url with deuteranomaly and go to that.</span>

<span class="c1">There, you get this image:</span>

<span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 624.00px; height: 350.67px;">![deuteranomaly.png](images/image5.png)</span>

<span class="c1"></span>

<span class="c1">You download this picture but what you download is a text file named “deuteranomaly.txt” and near the beginning is the string:</span>

<span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 638.50px; height: 86.00px;">![](images/image1.png)</span>

<span class="c1">To solve this part of the challenge, I first googled “Fuzyll DEFCON finals challenges.” I find a github page:</span>

<span class="c5">[https://github.com/fuzyll/defcon-vm](https://www.google.com/url?q=https://github.com/fuzyll/defcon-vm&sa=D&ust=1543614497361000)</span><span class="c1"> </span>

<span class="c1"></span>

<span class="c1">Looking through the page there are a lot of challenges listed. But remembering what his clue said, the first problem he got at defcon finals is something he can’t see very well. Deuteranomaly is a type of red-green color blindness. Are there any specific names of a challenge on there that is an object that is red and green, like a strawberry?</span>

<span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 632.67px; height: 54.50px;">![](images/image4.png)</span>

<span class="c1">Pretty sure tomatoes are red and green. So I tried that and what do you know it works!</span>

<span class="c1">We get to</span>

<span class="c5">[http://fuzyll.com/files/csaw2016/tomato](https://www.google.com/url?q=http://fuzyll.com/files/csaw2016/tomato&sa=D&ust=1543614497362000)</span><span class="c1"> </span>

<span class="c1">And then…</span>

<span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 409.50px; height: 114.92px;">![](images/image10.png)</span>

<span class="c1">I didn’t know what to do here. So… I decided to do something that probably nobody else did. I guessed the next page. I wrote a small python script to brute force a word list for the next filename on the website. I figured that since “tomato” is a common English word, maybe the next filename is or even better yet, the flag file page is named by a common English word. Either way, it shouldn’t take long to test the theory out and since I don’t know what else to do, screw it. Here is the python script I wrote:</span>

<span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 503.00px; height: 259.00px;">![](images/image6.png)</span>

<span class="c1">The word list I used (one of them in this repo):</span>

<span class="c5">[https://github.com/first20hours/google-10000-english](https://www.google.com/url?q=https://github.com/first20hours/google-10000-english&sa=D&ust=1543614497362000)</span><span class="c1"> </span>

<span class="c1"></span>

<span class="c1">I find viable options:</span>

*   <span class="c1">start</span>
*   <span class="c1">tomato</span>
*   <span class="c1">jade</span>

<span class="c1"></span>

<span class="c1">Hm… What is at /jade? This picture is:</span>

<span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 624.00px; height: 276.00px;">![jade.png](images/image9.jpg)</span>

<span class="c1"></span>

<span class="c1">Convert the image to a text file and you find the following message:</span>

<span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 624.00px; height: 85.33px;">![](images/image2.png)</span>

<span class="c1"></span>

<span class="c8">Reverse google image search the picture and you find out the name of these ruins is “</span><span class="c11">Wiñay Wayna</span><span class="c4">” and the only ASCII version is “Winay Wayna.”</span>

<span class="c4">So at /winaywayna you find the following message:</span>

<span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 617.50px; height: 69.00px;">![](images/image3.png)</span>
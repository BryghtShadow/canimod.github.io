---
layout: default
title: Object data
intro: This page explains how the game stores and parses object data. This is an advanced guide for mod developers.
---

## Reading the raw data

### Source
Objects are stored in `Content\Data\ObjectInformation.xnb`, which can be unpacked using
[XNB Extract by Drogean](http://community.playstarbound.com/threads/modding-guides-and-general-modding-discussion-redux.109131/).
Here's the raw data (as of 1.1.1) for reference:

```yaml
content:  #!Dictionary<Int32,String>
    0: "Weeds/0/-1/Basic/A bunch of obnoxious weeds." #!String
    2: "Stone/0/-300/Basic/A useful material when broken with the Pickaxe." #!String
    4: "Stone/0/-300/Basic/A useful material when chopped with the axe." #!String
    16: "Wild Horseradish/50/5/Basic -81/A spicy root found in the spring." #!String
    18: "Daffodil/30/0/Basic -81/A traditional spring flower that makes a nice gift." #!String
    20: "Leek/60/16/Basic -81/A tasty relative of the onion." #!String
    22: "Dandelion/40/10/Basic -81/Not the prettiest flower, but the leaves make a good salad." #!String
    24: "Parsnip/35/10/Basic -75/A spring tuber closely related to the carrot. It has an earthy taste and is full of nutrients." #!String
    30: "Lumber/2/10/Basic/A versatile resource used for building and fuel." #!String
    60: "Emerald/250/-300/Minerals -2/A precious stone with a brilliant green color." #!String
    62: "Aquamarine/180/-300/Minerals -2/A shimmery blue-green gem ." #!String
    64: "Ruby/250/-300/Minerals -2/A precious stone that is sought after for its rich color and beautiful luster." #!String
    66: "Amethyst/100/-300/Minerals -2/A purple variant of quartz." #!String
    68: "Topaz/80/-300/Minerals -2/Fairly common but still prized for its beauty." #!String
    70: "Jade/200/-300/Minerals -2/A pale green ornamental stone." #!String
    72: "Diamond/750/-300/Minerals -2/A rare and valuable gem." #!String
    74: "Prismatic Shard/2000/-300/Minerals -2/A very rare and powerful substance with unknown origins." #!String
    75: "Stone/50/-300/Basic/..." #!String
    76: "Stone/50/-300/Basic/..." #!String
    77: "Stone/50/-300/Basic/..." #!String
    78: "Cave Carrot/25/12/Basic -81/A starchy snack found in caves. It helps miners work longer." #!String
    80: "Quartz/25/-300/Minerals -2/A clear crystal commonly found in caves and mines." #!String
    82: "Fire Quartz/100/-300/Minerals -2/A glowing red crystal commonly found near hot lava." #!String
    84: "Frozen Tear/75/-300/Minerals -2/A crystal fabled to be the frozen tears of a yeti." #!String
    86: "Earth Crystal/50/-300/Minerals -2/A resinous substance found near the surface." #!String
    88: "Coconut/100/-300/Basic -79/A seed of the coconut palm. It has many culinary uses." #!String
    90: "Cactus Fruit/75/30/Basic -79/The sweet fruit of the prickly pear cactus." #!String
    92: "Sap/2/-1/Basic -81/A fluid obtained from trees." #!String
    93: "Torch/5/-300/Crafting/Provides a modest amount of light." #!String
    94: "Spirit Torch/5/-300/Crafting/It's unclear where the blue color comes from..." #!String
    96: "Dwarf Scroll I/1/-300/Arch/A yellowed scroll of parchment filled with dwarven script. This one's tied with a red bow.//Set Dwarf 96 97 98 99" #!String
    97: "Dwarf Scroll II/1/-300/Arch/A yellowed scroll of parchment filled with dwarven script. This one's tied with a green ribbon.//Set Dwarf 96 97 98 99" #!String
    98: "Dwarf Scroll III/1/-300/Arch/A yellowed scroll of parchment filled with dwarven script. This one's tied with a blue rope.//Set Dwarf 96 97 98 99" #!String
    99: "Dwarf Scroll IV/1/-300/Arch/A yellowed scroll of parchment filled with dwarven script. This one's tied with a golden chain.//Set Dwarf 96 97 98 99" #!String
    100: "Chipped Amphora/40/-300/Arch/An ancient vessel made of ceramic material. Used to transport both dry and wet goods./Town .04/Item 3 461" #!String
    101: "Arrowhead/40/-300/Arch/A crudely fashioned point used for hunting./Mountain .02 Forest .02 BusStop .02/Debris 2 30 14" #!String
    102: "Lost Book/50/-300/asdf/Writings from a wide variety of time periods./Town .05/Note" #!String
    103: "Ancient Doll/60/-300/Arch/An ancient doll covered in grime. This doll may have been used as a toy, a decoration, or a prop in some kind of ritual./Mountain .04 Forest .03 BusStop .03 Town .01/Money 1 250" #!String
    104: "Elvish Jewelry/200/-300/Arch/Dirty but still beautiful. On the side is a flowing script thought by some to be the ancient language of the elves. No Elvish bones have ever been found./Forest .01/Debris 1 20 6" #!String
    105: "Chewing Stick/50/-300/Arch/Ancient people chewed on these to keep their teeth clean./Mountain .02 Town .01 Forest .02/Decor 10 28" #!String
    106: "Ornamental Fan/300/-300/Arch/This exquisute fan most likely belonged to a noblewoman. Historians believe that the valley was a popular sixth-era vacation spot for the wealthy./Beach .02 Town .008 Forest .01/Money 1 300" #!String
    107: "Dinosaur Egg/350/-300/Arch/A giant dino egg... The entire shell is still intact!/Mine .01 Mountain .008/Item 1 107" #!String
    108: "Rare Disc/300/-300/Arch/A heavy black disc studded with peculiar red stones. When you hold it, you're overwhelmed with a feeling of dread./UndergroundMine .01/Decor 1 29" #!String
    109: "Ancient Sword/100/-300/Arch/It's the remains of an ancient sword. Most of the blade has turned to rust, but the hilt is very finely crafted./Forest .01 Mountain .008/Debris 1 30 2" #!String
    110: "Rusty Spoon/25/-300/Arch/A plain old spoon, probably ten years old. Not very interesting./Town .05/Debris 5 30 2" #!String
    111: "Rusty Spur/25/-300/Arch/An old spur that was once attached to a cowboy's boot. People must have been raising animals in this area for many generations./Farm .1/Money 1 100" #!String
    112: "Rusty Cog/25/-300/Arch/A well preserved cog that must have been part of some ancient machine. This could be dwarven technology./Mountain .05/Debris 1 20 4" #!String
    113: "Chicken Statue/50/-300/Arch/It's a statue of a chicken on a bronze base. The ancient people of this area must have been very fond of chickens./Farm .1/Decor 5 31" #!String
    114: "Ancient Seed/5/-300/Arch/It's a dry old seed from some ancient plant. By all appearances it's long since dead.../Forest .01 Mountain .01/Seeds 9" #!String
    115: "Prehistoric Tool/50/-300/Arch/Some kind of gnarly old digging tool./Mountain .03 Forest .03 BusStop .04/Debris 1 30 12" #!String
    116: "Dried Starfish/40/-300/Arch/A starfish from the primordial ocean. It's an unusually pristine specimen!/Beach .1/Money 1 200" #!String
    117: "Anchor/100/-300/Arch/It may have belonged to ancient pirates./Beach .05/Item 1 289" #!String
    118: "Glass Shards/20/-300/Arch/A mixture of glass shards smoothed by centuries of ocean surf. These could have belonged to an ancient mosaic or necklace./Beach .1/Item 1 462" #!String
    119: "Bone Flute/100/-300/Arch/It's a prehistoric wind instrument carved from an animal's bone. It produces an eerie tone./Mountain .01 Forest .01 UndergroundMine .02 Town .005/Recipe 2 Flute_Block 150" #!String
    120: "Prehistoric Handaxe/50/-300/Arch/One of the earliest tools employed by humans. This \"crude\" tool was created by striking one rock with another to form a sharp edge./Mountain .05 Forest .05 BusStop .05/Item 1 294" #!String
    121: "Dwarvish Helm/100/-300/Arch/It's one of the helmets commonly worn by dwarves. The thick metal plating protects them from falling debris and stalactites./UndergroundMine .01/Debris 1 50 0" #!String
    122: "Dwarf Gadget/200/-300/Arch/It's a piece of the advanced technology once known to the dwarves. It's still glowing and humming, but you're unable to understand how it works./UndergroundMine .001/Money 1 500" #!String
    123: "Ancient Drum/100/-300/Arch/It's a drum made from wood and animal skin. It has a low, reverberating tone./BusStop .01 Forest .01 UndergroundMine .02 Town .005/Recipe 2 Drum_Block 300" #!String
    124: "Golden Mask/500/-300/Arch/A creepy golden mask probably used in an ancient magic ritual. A socket in the forehead contains a large purple gemstone./Desert .04/Money 1 1000" #!String
    125: "Golden Relic/250/-300/Arch/It's a golden slab with heiroglyphs and pictures emblazoned onto the front./Desert .08/Debris 1 40 6" #!String
    126: "Strange Doll/1000/-300/Arch/???/Farm .001 Town .001 Mountain .001 Forest .001 BusStop .001 Beach .001 UndergroundMine .001/Item 1 126" #!String
    127: "Strange Doll/1000/-300/Arch/???/Farm .001 Town .001 Mountain .001 Forest .001 BusStop .001 Beach .001 UndergroundMine .001/Item 1 127" #!String
    128: "Pufferfish/200/-40/Fish -4/Inflates when threatened./Day^Summer" #!String
    129: "Anchovy/30/5/Fish -4/A small silver fish found in the ocean./Day Night^Spring Fall" #!String
    130: "Tuna/100/15/Fish -4/A large fish that lives in the ocean./Day^Summer Winter" #!String
    131: "Sardine/40/5/Fish -4/A common ocean fish./Day^Spring Summer Fall Winter" #!String
    132: "Bream/45/5/Fish -4/A fairly common river fish that becomes active at night./Night^Spring Summer Fall Winter" #!String
    136: "Largemouth Bass/100/15/Fish -4/A popular fish that lives in lakes./Day^Spring Summer Fall Winter" #!String
    137: "Smallmouth Bass/50/10/Fish -4/A freshwater fish that is very sensitive to pollution./Day Night^Spring Fall" #!String
    138: "Rainbow Trout/65/10/Fish -4/A freshwater trout with colorful markings./Day^Summer" #!String
    139: "Salmon/75/15/Fish -4/Swims upstream to lay its eggs./Day^Fall" #!String
    140: "Walleye/105/12/Fish -4/A freshwater fish caught at night./Night^Fall Winter" #!String
    141: "Perch/55/10/Fish -4/A freshwater fish of the winter./Day Night^Winter" #!String
    142: "Carp/30/5/Fish -4/A common pond fish./Day Night^Spring Summer Fall" #!String
    143: "Catfish/200/20/Fish -4/An uncommon fish found in streams./Day^Spring Fall Winter" #!String
    144: "Pike/100/15/Fish -4/A freshwater fish that's difficult to catch./Day Night^Summer Winter" #!String
    145: "Sunfish/30/5/Fish -4/A common river fish./Day^Spring Summer" #!String
    146: "Red Mullet/75/10/Fish -4/Long ago these were kept as pets./Day^Summer Winter" #!String
    147: "Herring/30/5/Fish -4/A common ocean fish./Day Night^Spring Winter" #!String
    148: "Eel/85/12/Fish -4/A long, slippery little fish./Night^Spring Fall" #!String
    149: "Octopus/150/-300/Fish -4/A mysterious and intelligent creature./Day^Summer" #!String
    150: "Red Snapper/50/10/Fish -4/A popular fish with a nice red color./Day^Summer Fall Winter" #!String
    151: "Squid/80/10/Fish -4/A deep sea creature that can grow to enormous size./Day^Winter" #!String
    152: "Seaweed/20/5/Fish/It can be used in cooking./Day Night^Spring Summer Fall Winter" #!String
    153: "Green Algae/15/5/Fish/It's really slimy./Day Night^Spring Summer Fall Winter" #!String
    154: "Sea Cucumber/75/-10/Fish -4/A slippery, slimy creature found on the ocean floor./Day^Fall Winter" #!String
    155: "Super Cucumber/250/50/Fish -4/A rare, purple variety of sea cucumber./Night^Summer Fall" #!String
    156: "Ghostfish/45/15/Fish -4/A pale, blind fish found in underground lakes./Day Night^Spring Summer Fall Winter" #!String
    157: "White Algae/25/8/Fish/It's super slimy./Day Night^Spring Summer Fall Winter" #!String
    158: "Stonefish/300/-300/Fish -4/A bizarre fish that's shaped like a brick./Day Night^Spring Summer Fall Winter" #!String
    159: "Crimsonfish/1500/15/Fish -4/Lives deep in the ocean but likes to lay its eggs in the warm summer water./Day^Winter" #!String
    160: "Angler/900/10/Fish -4/Uses a bioluminescent dangler to attract prey./Day Night^Spring Summer Fall Winter" #!String
    161: "Ice Pip/500/15/Fish -4/A rare fish that thrives in extremely cold conditions./Day Night^Spring Summer Fall Winter" #!String
    162: "Lava Eel/700/20/Fish -4/It can somehow survive in pools of red-hot lava./Day Night^Spring Summer Fall Winter" #!String
    163: "Legend/5000/200/Fish -4/The king of all fish! They said he'd never be caught./Day^Winter" #!String
    164: "Sandfish/75/5/Fish -4/It tries to hide using camouflage./Day Night^Spring Summer Fall Winter" #!String
    165: "Scorpion Carp/150/-50/Fish -4/It's like a regular carp but with a sharp stinger./Day Night^Spring Summer Fall Winter" #!String
    166: "Treasure Chest/5000/-300/Basic/Wow, it's loaded with treasure! This is sure to fetch a good price./Day Night^Spring Summer Fall Winter" #!String
    167: "Joja Cola/25/5/Fish -20/The flagship product of Joja corporation./drink/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    168: "Trash/0/-300/Fish -20/It's junk./Day Night^Spring Summer Fall Winter" #!String
    169: "Driftwood/0/-300/Fish -20/A piece of wood from the sea./Day Night^Spring Summer Fall Winter" #!String
    170: "Broken Glasses/0/-300/Fish -20/It looks like someone lost their glasses. They're busted./Day Night^Spring Summer Fall Winter" #!String
    171: "Broken CD/0/-300/Fish -20/It's a JojaNet 2.0 trial CD. They must've made a billion of these things./Day Night^Spring Summer Fall Winter" #!String
    172: "Soggy Newspaper/0/-300/Fish -20/This is trash./Day Night^Spring Summer Fall Winter" #!String
    174: "Large Egg/95/15/Basic -5/It's an uncommonly large white egg!" #!String
    176: "Egg/50/10/Basic -5/A regular white chicken egg." #!String
    178: "Hay/0/-300/Basic/Dried grass used as animal food." #!String
    180: "Egg/50/10/Basic -5/A regular brown chicken egg." #!String
    182: "Large Egg/95/15/Basic -5/It's an uncommonly large brown egg!" #!String
    184: "Milk/125/15/Basic -6/A jug of cow's milk./drink/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    186: "Large Milk/190/20/Basic -6/A large jug of cow's milk./drink/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    188: "Green Bean/40/10/Basic -75/A juicy little bean with a cool, crisp snap." #!String
    190: "Cauliflower/175/30/Basic -75/Valuable, but slow-growing. Despite its pale color, the florets are packed with nutrients." #!String
    192: "Potato/80/10/Basic -75/A widely cultivated tuber." #!String
    194: "Fried Egg/35/20/Cooking -7/Sunny-side up./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    195: "Omelet/125/40/Cooking -7/It's super fluffy./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    196: "Salad/110/45/Cooking -7/A healthy garden salad./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    197: "Cheese Cauliflower/300/55/Cooking -7/It smells great!/food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    198: "Baked Fish/100/30/Cooking -7/Baked fish on a bed of herbs./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    199: "Parsnip Soup/120/34/Cooking -7/It's fresh and hearty./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    200: "Vegetable Medley/120/66/Cooking -7/This is very nutritious./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    201: "Complete Breakfast/350/80/Cooking -7/You'll feel ready to take on the world!/food/2 0 0 0 0 0 0 50 0 0 0/600" #!String
    202: "Fried Calamari/150/32/Cooking -7/It's so chewy./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    203: "Strange Bun/225/40/Cooking -7/What's inside?/food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    204: "Lucky Lunch/250/40/Cooking -7/A special little meal./food/0 0 0 0 3 0 0 0 0 0 0/960" #!String
    205: "Fried Mushroom/200/54/Cooking -7/Earthy and aromatic./food/0 0 0 0 0 0 0 0 0 0 0 2/600" #!String
    206: "Pizza/300/60/Cooking -7/It's popular for all the right reasons./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    207: "Bean Hotpot/100/50/Cooking -7/It sure is healthy./food/0 0 0 0 0 0 2 0 0 0 0/600" #!String
    208: "Glazed Yams/200/80/Cooking -7/Sweet and satisfying... The sugar gives it a hint of caramel./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    209: "Carp Surprise/150/36/Cooking -7/It's bland and oily./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    210: "Hashbrowns/120/36/Cooking -7/Crispy and golden-brown!/food/1 0 0 0 0 0 0 0 0 0 0/480" #!String
    211: "Pancakes/80/36/Cooking -7/A double stack of fluffy, soft pancakes./food/0 0 0 0 0 2 0 0 0 0 0/960" #!String
    212: "Salmon Dinner/300/50/Cooking -7/The lemon spritz makes it special./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    213: "Fish Taco/500/66/Cooking -7/It smells delicious./food/0 2 0 0 0 0 0 0 0 0 0/600" #!String
    214: "Crispy Bass/150/36/Cooking -7/Wow, the breading is perfect./food/0 0 0 0 0 0 0 0 64 0 0/600" #!String
    215: "Pepper Poppers/200/52/Cooking -7/Spicy breaded peppers filled with cheese./food/2 0 0 0 0 0 0 0 0 1 0/600" #!String
    216: "Bread/60/20/Cooking -7/A crusty baguette./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    218: "Tom Kha Soup/250/70/Cooking -7/These flavors are incredible!/food/2 0 0 0 0 0 0 30 0 0 0/600" #!String
    219: "Trout Soup/100/40/Cooking -7/Pretty salty./food/0 1 0 0 0 0 0 0 0 0 0/400" #!String
    220: "Chocolate Cake/200/60/Cooking -7/Rich and moist with a thick fudge icing./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    221: "Pink Cake/480/100/Cooking -7/There's little heart candies on top./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    222: "Rhubarb Pie/400/86/Cooking -7/Mmm, tangy and sweet!/food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    223: "Cookie/140/36/Cooking -7/Very chewy./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    224: "Spaghetti/120/30/Cooking -7/An old favorite./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    225: "Fried Eel/120/30/Cooking -7/Greasy but flavorful./food/0 0 0 0 1 0 0 0 0 0 0/600" #!String
    226: "Spicy Eel/175/46/Cooking -7/It's really spicy! Be careful./food/0 0 0 0 1 0 0 0 0 1 0/600" #!String
    227: "Sashimi/75/30/Cooking -7/Raw fish sliced into thin pieces./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    228: "Maki Roll/220/40/Cooking -7/Fish and rice wrapped in seaweed./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    229: "Tortilla/50/20/Cooking -7/Can be used as a vessel for food or eaten by itself./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    230: "Red Plate/400/96/Cooking -7/Full of antioxidants./food/0 0 0 0 0 0 0 50 0 0 0/300" #!String
    231: "Eggplant Parmesan/200/70/Cooking -7/Tangy, cheesy, and wonderful./food/0 0 1 0 0 0 0 0 0 0 3/400" #!String
    232: "Rice Pudding/260/46/Cooking -7/It's creamy, sweet, and fun to eat./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    233: "Ice Cream/120/40/Cooking -7/It's hard to find someone who doesn't like this./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    234: "Blueberry Tart/150/50/Cooking -7/It's subtle and refreshing./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    235: "Autumn's Bounty/350/88/Cooking -7/A taste of the season./food/0 0 0 0 0 2 0 0 0 0 2/660" #!String
    236: "Pumpkin Soup/300/80/Cooking -7/A seasonal favorite./food/0 0 0 0 2 0 0 0 0 0 2/660" #!String
    237: "Super Meal/220/64/Cooking -7/It's a really energizing meal./food/0 0 0 0 0 0 0 40 0 1 0/300" #!String
    238: "Cranberry Sauce/120/50/Cooking -7/A festive treat./food/0 0 2 0 0 0 0 0 0 0 0/300" #!String
    239: "Stuffing/165/68/Cooking -7/Ahh... the smell of warm bread and sage./food/0 0 0 0 0 0 0 0 0 0 2/480" #!String
    240: "Farmer's Lunch/150/80/Cooking -7/This'll keep you going./food/3 0 0 0 0 0 0 0 0 0 0/480" #!String
    241: "Survival Burger/180/50/Cooking -7/A convenient snack for the explorer./food/0 0 0 0 0 3 0 0 0 0 0/480" #!String
    242: "Dish O' The Sea/220/60/Cooking -7/This'll keep you warm in the cold sea air./food/0 3 0 0 0 0 0 0 0 0 0/480" #!String
    243: "Miner's Treat/200/50/Cooking -7/This should keep your energy up./food/0 0 3 0 0 0 0 0 32 0 0/480" #!String
    244: "Roots Platter/100/50/Cooking -7/This'll get you digging for more./food/0 0 0 0 0 0 0 0 0 0 0 3/480" #!String
    245: "Sugar/50/10/Basic/Adds sweetness to pastries and candies. Too much can be unhealthy." #!String
    246: "Wheat Flour/50/5/Basic/A common cooking ingredient made from crushed wheat seeds." #!String
    247: "Oil/100/5/Basic/All purpose cooking oil." #!String
    248: "Garlic/60/8/Basic -75/Adds a wonderful zestiness to dishes. High quality garlic can be pretty spicy." #!String
    250: "Kale/110/20/Basic -75/The waxy leaves are great in soups and stir frys." #!String
    252: "Rhubarb/220/-300/Basic -79/The stalks are extremely tart, but make a great dessert when sweetened." #!String
    254: "Melon/250/45/Basic -79/A cool, sweet summer treat." #!String
    256: "Tomato/60/8/Basic -75/Rich and slightly tangy, the Tomato has a wide variety of culinary uses." #!String
    257: "Morel/150/8/Basic -81/Sought after for its unique nutty flavor." #!String
    258: "Blueberry/50/10/Basic -79/A popular berry reported to have many health benefits. The blue skin has the highest nutrient concentration." #!String
    259: "Fiddlehead Fern/90/10/Basic -75/The young shoots are an edible specialty." #!String
    260: "Hot Pepper/40/5/Basic -79/Fiery hot with a hint of sweetness." #!String
    262: "Wheat/25/-300/Basic -75/One of the most widely cultivated grains. Makes a great flour for breads and cakes." #!String
    264: "Radish/90/18/Basic -75/A crisp and refreshing root vegetable with hints of pepper when eaten raw." #!String
    266: "Red Cabbage/260/30/Basic -75/Often used in salads and coleslaws. The color can range from purple to blue to green-yellow depending on soil conditions." #!String
    268: "Starfruit/750/50/Basic -79/An extremely juicy fruit that grows in hot, humid weather. Slightly sweet with a sour undertone." #!String
    270: "Corn/50/10/Basic -75/One of the most popular grains. The sweet, fresh cobs are a summer favorite." #!String
    272: "Eggplant/60/8/Basic -75/A rich and wholesome relative of the tomato. Delicious fried or stewed." #!String
    274: "Artichoke/160/12/Basic -75/The bud of a thistle plant. The spiny outer leaves conceal a fleshy, filling interior." #!String
    276: "Pumpkin/320/-300/Basic -75/A fall favorite, grown for its crunchy seeds and delicately flavored flesh. As a bonus, the hollow shell can be carved into a festive decoration." #!String
    278: "Bok Choy/80/10/Basic -75/The leafy greens and fibrous stalks are healthy and delicious." #!String
    280: "Yam/160/18/Basic -75/A starchy tuber with a lot of culinary versatility." #!String
    281: "Chanterelle/160/30/Basic -81/A tasty mushroom with a fruity smell and slightly peppery flavor." #!String
    282: "Cranberries/75/15/Basic -79/These tart red berries are a traditional winter food." #!String
    283: "Holly/80/-15/Basic -81/The leaves and bright red berries make a popular winter decoration." #!String
    284: "Beet/100/12/Basic -75/A sweet and earthy root vegatable. As a bonus, the leaves make a great salad." #!String
    286: "Cherry Bomb/50/-300/Crafting -8/Generates a small explosion. Stand back!" #!String
    287: "Bomb/50/-300/Crafting -8/Generates an explosion. Watch out!" #!String
    288: "Mega Bomb/50/-300/Crafting -8/Generates a powerful explosion. Use with extreme caution." #!String
    290: "Stone/50/-300/Basic/..." #!String
    294: "Twig/1/-300/Crafting/..." #!String
    295: "Twig/1/-300/Crafting/..." #!String
    296: "Salmonberry/5/10/Basic -79/A spring-time berry with the flavor of the forest." #!String
    297: "Grass Starter/50/-300/Crafting/Place this on your farm to start a new patch of grass." #!String
    298: "Hardwood Fence/10/-300/Crafting -8/The most durable type of fence." #!String
    299: "Amaranth Seeds/35/-300/Seeds -74/Plant these in the fall. Takes 7 days to grow. Harvest with the scythe." #!String
    300: "Amaranth/150/20/Basic -75/A purple grain cultivated by an ancient civilization." #!String
    301: "Grape Starter/30/-300/Seeds -74/Plant these in the fall. Takes 10 days to grow, but keeps producing after that. Grows on a trellis." #!String
    302: "Hops Starter/30/-300/Seeds -74/Plant these in the summer. Takes 11 days to grow, but keeps producing after that. Grows on a trellis." #!String
    303: "Pale Ale/300/20/Basic -26/Drink in moderation./drink/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    304: "Hops/25/18/Basic -75/A bitter, tangy flower used to flavor beer." #!String
    305: "Void Egg/65/15/Basic -5/A jet-black egg with red flecks. It's warm to the touch." #!String
    306: "Mayonnaise/190/-300/Basic -26/It looks spreadable." #!String
    307: "Duck Mayonnaise/375/-300/Basic -26/It's a rich, yellow mayonnaise." #!String
    308: "Void Mayonnaise/275/-30/Basic -26/A thick, black paste that smells like burnt hair." #!String
    309: "Acorn/20/-300/Crafting -74/Place this on your farm to plant an oak tree." #!String
    310: "Maple Seed/5/-300/Crafting -74/Place this on your farm to plant a maple tree." #!String
    311: "Pine Cone/5/-300/Crafting -74/Place this on your farm to plant a pine tree." #!String
    313: "Weeds/50/-300/Crafting/..." #!String
    314: "Weeds/50/-300/Crafting/..." #!String
    315: "Weeds/50/-300/Crafting/..." #!String
    316: "Weeds/50/-300/Crafting/..." #!String
    317: "Weeds/50/-300/Crafting/..." #!String
    318: "Weeds/50/-300/Crafting/..." #!String
    319: "Weeds/50/-300/Crafting/..." #!String
    320: "Weeds/50/-300/Crafting/..." #!String
    321: "Weeds/50/-300/Crafting/..." #!String
    322: "Wood Fence/1/-300/Crafting -8/Keeps grass and animals contained!" #!String
    323: "Stone Fence/2/-300/Crafting -8/Lasts longer than a wood fence." #!String
    324: "Iron Fence/6/-300/Crafting -8/Lasts longer than a stone fence." #!String
    325: "Gate/4/-300/Crafting -8/Allows you to pass through a fence." #!String
    326: "Dwarvish Translation Guide/50/-300/Crafting -8/Teaches you dwarvish." #!String
    328: "Wood Floor/1/-300/Crafting -24/Place on the ground to create paths or to decorate your floors." #!String
    329: "Stone Floor/1/-300/Crafting -24/Place on the ground to create paths or to spruce up your floors." #!String
    330: "Clay/20/-300/Basic -16/Used in crafting and construction." #!String
    331: "Weathered Floor/1/-300/Crafting -24/Place on the ground to create paths or to spruce up your floors." #!String
    333: "Crystal Floor/1/-300/Crafting -24/Place on the ground to create paths or to spruce up your floors." #!String
    334: "Copper Bar/60/-300/Basic -15/A bar of pure copper." #!String
    335: "Iron Bar/120/-300/Basic -15/A bar of pure iron." #!String
    336: "Gold Bar/250/-300/Basic -15/A bar of pure gold." #!String
    337: "Iridium Bar/1000/-300/Basic -15/A bar of pure iridium." #!String
    338: "Refined Quartz/50/-300/Basic -15/A more pure form of quartz." #!String
    340: "Honey/100/-300/Basic -26/It's a sweet syrup produced by bees." #!String
    341: "Tea Set/200/-300/Basic -24/Fine porcelain." #!String
    342: "Pickles/100/-300/Basic -26/A jar of your home-made pickles." #!String
    343: "Stone/100/-300/Basic/Stone." #!String
    344: "Jelly/160/-300/Basic -26/Gooey." #!String
    346: "Beer/200/20/Basic -26/Drink in moderation./drink/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    347: "Rare Seed/200/-300/Seeds -74/Sow in fall. Takes all season to grow." #!String
    348: "Wine/400/20/Basic -26/Drink in moderation./drink/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    349: "Energy Tonic/500/200/Crafting/Restores a lot of energy./drink/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    350: "Juice/150/30/Basic -26/A sweet, nutritious beverage./drink/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    351: "Muscle Remedy/500/20/Crafting/When you've pushed your body too hard, drink this to remove 'Exhaustion'./drink/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    368: "Basic Fertilizer/2/-300/Basic -19/Improves soil quality a little, increasing your chance to grow quality crops. Mix into tilled soil." #!String
    369: "Quality Fertilizer/10/-300/Basic -19/Improves soil quality, increasing your chance to grow quality crops. Mix into tilled soil." #!String
    370: "Basic Retaining Soil/4/-300/Basic -19/This soil has a chance of staying watered overnight. Mix into tilled soil." #!String
    371: "Quality Retaining Soil/5/-300/Basic -19/This soil has a good chance of staying watered overnight. Mix into tilled soil." #!String
    372: "Clam/50/-300/Basic -23/Someone lived here once." #!String
    373: "Golden Pumpkin/2500/-300/Basic/It's valuable but has no other purpose." #!String
    376: "Poppy/140/18/Basic -80/In addition to its colorful flower, the Poppy has culinary and medicinal uses." #!String
    378: "Copper Ore/5/-300/Basic -15/A common ore that can be smelted into bars." #!String
    380: "Iron Ore/10/-300/Basic -15/A fairly common ore that can be smelted into bars." #!String
    382: "Coal/15/-300/Basic -15/A combustible rock that is useful for crafting and smelting." #!String
    384: "Gold Ore/25/-300/Basic -15/A precious ore that can be smelted into bars." #!String
    386: "Iridium Ore/100/-300/Basic -15/An exotic ore with many curious properties. Can be smelted into bars." #!String
    388: "Wood/2/-300/Basic -16/A sturdy, yet flexible plant material with a wide variety of uses." #!String
    390: "Stone/2/-300/Basic -16/A common material with many uses in crafting and building." #!String
    392: "Nautilus Shell/120/-300/Basic -23/An ancient shell." #!String
    393: "Coral/80/-300/Basic -23/A colony of tiny creatures that clump together to form beautiful structures." #!String
    394: "Rainbow Shell/300/-300/Basic -23/It's a very beautiful shell." #!String
    395: "Coffee/150/1/Crafting/It smells delicious. This is sure to give you a boost./drink/0 0 0 0 0 0 0 0 0 1 0/120" #!String
    396: "Spice Berry/80/10/Basic -79/It fills the air with a pungent aroma." #!String
    397: "Sea Urchin/160/-300/Basic -23/A slow-moving, spiny creature that some consider a delicacy." #!String
    398: "Grape/80/15/Basic -79/A sweet cluster of fruit." #!String
    399: "Spring Onion/8/5/Basic -81/These grow wild during the spring." #!String
    400: "Strawberry/120/20/Basic -79/A sweet, juicy favorite with an appealing red color." #!String
    401: "Straw Floor/1/-300/Crafting -24/Place on the ground to create paths or to spruce up your floors." #!String
    402: "Sweet Pea/50/0/Basic -80/A fragrant summer flower." #!String
    403: "Field Snack/20/18/Crafting/A quick snack to fuel the hungry forager." #!String
    404: "Common Mushroom/40/15/Basic -81/Slightly nutty, with good texture." #!String
    405: "Wood Path/1/-300/Crafting -24/Place on the ground to create paths or to spruce up your floors." #!String
    406: "Wild Plum/80/10/Basic -79/Tart and juicy with a pungent aroma." #!String
    407: "Gravel Path/1/-300/Crafting -24/Place on the ground to create paths or to spruce up your floors." #!String
    408: "Hazelnut/90/12/Basic -81/That's one big hazelnut!" #!String
    409: "Crystal Path/1/-300/Crafting -24/Place on the ground to create paths or to spruce up your floors." #!String
    410: "Blackberry/20/10/Basic -79/An early-fall treat." #!String
    411: "Cobblestone Path/1/-300/Crafting -24/Place on the ground to create paths or to spruce up your floors." #!String
    412: "Winter Root/70/10/Basic -81/A starchy tuber." #!String
    413: "Blue Slime Egg/1750/-300/Basic/Can be hatched in a slime incubator." #!String
    414: "Crystal Fruit/150/25/Basic -79/A delicate fruit that pops up from the snow." #!String
    415: "Stepping Stone Path/1/-300/Crafting -24/Place on the ground to create paths or to spruce up your floors." #!String
    416: "Snow Yam/100/12/Basic -81/This little yam was hiding beneath the snow." #!String
    417: "Sweet Gem Berry/3000/-300/Basic -17/It's by far the sweetest thing you've ever smelled." #!String
    418: "Crocus/60/0/Basic -80/A flower that can bloom in the winter." #!String
    419: "Vinegar/100/5/Basic/An aged fermented liquid used in many cooking recipes./drink" #!String
    420: "Red Mushroom/75/-20/Basic -81/A spotted mushroom sometimes found in caves." #!String
    421: "Sunflower/80/18/Basic -80/A common misconception is that the flower turns so it's always facing the sun." #!String
    422: "Purple Mushroom/250/50/Basic -81/A rare mushroom found deep in caves." #!String
    423: "Rice/100/5/Basic/A basic grain often served under vegetables." #!String
    424: "Cheese/200/50/Basic -26/It's your basic cheese." #!String
    425: "Fairy Seeds/100/-300/Seeds -74/Plant in fall. Takes 12 days to produce a mysterious flower. Assorted Colors." #!String
    426: "Goat Cheese/375/50/Basic -26/Soft cheese made from goat's milk." #!String
    427: "Tulip Bulb/10/-300/Seeds -74/Plant in spring. Takes 6 days to produce a colorful flower. Assorted colors." #!String
    428: "Cloth/470/-300/Basic -26/A bolt of fine wool cloth." #!String
    429: "Jazz Seeds/15/-300/Seeds -74/Plant in spring. Takes 7 days to produce a blue puffball flower." #!String
    430: "Truffle/625/5/Basic -17/A gourmet type of mushroom with a unique taste." #!String
    431: "Sunflower Seeds/20/-300/Seeds -74/Plant in summer or fall. Takes 8 days to produce a large sunflower. Yields more seeds at harvest." #!String
    432: "Truffle Oil/1065/15/Basic -26/A gourmet cooking ingredient." #!String
    433: "Coffee Bean/15/-300/Seeds -74/Plant in spring or summer to grow a coffee plant. Place five beans in a keg to make coffee." #!String
    434: "Stardrop/7777/100/Crafting/A mysterious fruit that empowers those who eat it. The flavor is like a dream... a powerful personal experience, yet difficult to describe to others." #!String
    436: "Goat Milk/225/25/Basic -6/The milk of a goat./drink/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    437: "Red Slime Egg/2500/-300/Basic/Can be hatched in a slime incubator." #!String
    438: "L. Goat Milk/345/35/Basic -6/A gallon of creamy goat's milk./drink/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    439: "Purple Slime Egg/5000/-300/Basic/Can be hatched in a slime incubator." #!String
    440: "Wool/340/-300/Basic -18/Soft, fluffy wool." #!String
    441: "Explosive Ammo/20/-300/Basic/Fire this with the slingshot." #!String
    442: "Duck Egg/95/15/Basic -5/It's still warm." #!String
    444: "Duck Feather/125/-300/Basic -18/It's so colorful." #!String
    446: "Rabbit's Foot/565/-300/Basic -18/Some say it's lucky." #!String
    449: "Stone Base/0/-300/asdf/A simple block of stone." #!String
    450: "Stone/0/-300/asdf/Stone." #!String
    452: "Weeds/0/-300/asdf/A cluster of dry old bushes." #!String
    453: "Poppy Seeds/50/-300/Seeds -74/Plant in summer. Produces a bright red flower in 7 days." #!String
    454: "Ancient Fruit/550/-300/Basic -79/It's been dormant for eons." #!String
    455: "Spangle Seeds/25/-300/Seeds -74/Plant in summer. Takes 8 days to produce a vibrant tropical flower. Assorted colors." #!String
    456: "Algae Soup/100/30/Cooking -7/It's a little slimy./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    457: "Pale Broth/150/50/Cooking -7/A delicate broth with a hint of sulfur./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    458: "Bouquet/100/-300/Basic/A gift that shows your romantic interest." #!String
    459: "Mead/200/30/Basic -26/A fermented beverage made from honey. Drink in moderation./drink/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    460: "Mermaid's Pendant/2500/-300/Basic/Give this to the person you want to marry." #!String
    461: "Decorative Pot/200/-300/Crafting/A replica of an ancient pot." #!String
    463: "Drum Block/100/-300/Crafting/Plays a drum sound when you walk past." #!String
    464: "Flute Block/100/-300/Crafting/Plays a flute sound when you walk past." #!String
    465: "Speed-Gro/20/-300/Basic -19/Stimulates leaf production. Guaranteed to increase growth rate by at least 10%. Mix into tilled soil." #!String
    466: "Deluxe Speed-Gro/40/-300/Basic -19/Stimulates leaf production. Guaranteed to increase growth rate by at least 25%. Mix into tilled soil." #!String
    472: "Parsnip Seeds/10/-300/Seeds -74/Plant these in the spring. Takes 4 days to mature." #!String
    473: "Bean Starter/30/-300/Seeds -74/Plant these in the spring. Takes 10 days to mature, but keeps producing after that. Yields multiple beans per harvest. Grows on a trellis." #!String
    474: "Cauliflower Seeds/40/-300/Seeds -74/Plant these in the spring. Takes 12 days to produce a large cauliflower." #!String
    475: "Potato Seeds/25/-300/Seeds -74/Plant these in the spring. Takes 6 days to mature, and has a chance of yielding multiple potatoes at harvest." #!String
    476: "Garlic Seeds/20/-300/Seeds -74/Plant these in the spring. Takes 4 days to mature." #!String
    477: "Kale Seeds/35/-300/Seeds -74/Plant these in the spring. Takes 6 days to mature. Harvest with the scythe." #!String
    478: "Rhubarb Seeds/50/-300/Seeds -74/Plant these in the spring. Takes 13 days to mature." #!String
    479: "Melon Seeds/40/-300/Seeds -74/Plant these in the summer. Takes 12 days to mature." #!String
    480: "Tomato Seeds/25/-300/Seeds -74/Plant these in the summer. Takes 11 days to mature, and continues to produce after first harvest." #!String
    481: "Blueberry Seeds/40/-300/Seeds -74/Plant these in the summer. Takes 13 days to mature, and continues to produce after first harvest." #!String
    482: "Pepper Seeds/20/-300/Seeds -74/Plant these in the summer. Takes 5 days to mature, and continues to produce after first harvest." #!String
    483: "Wheat Seeds/5/-300/Seeds -74/Plant these in the summer or fall. Takes 4 days to mature. Harvest with the scythe." #!String
    484: "Radish Seeds/20/-300/Seeds -74/Plant these in the summer. Takes 6 days to mature." #!String
    485: "Red Cabbage Seeds/50/-300/Seeds -74/Plant these in the summer. Takes 9 days to mature." #!String
    486: "Starfruit Seeds/200/-300/Seeds -74/Plant these in the summer. Takes 13 days to mature." #!String
    487: "Corn Seeds/75/-300/Seeds -74/Plant these in the summer or fall. Takes 14 days to mature, and continues to produce after first harvest." #!String
    488: "Eggplant Seeds/10/-300/Seeds -74/Plant these in the fall. Takes 5 days to mature, and continues to produce after first harvest." #!String
    489: "Artichoke Seeds/15/-300/Seeds -74/Plant these in the fall. Takes 8 days to mature." #!String
    490: "Pumpkin Seeds/50/-300/Seeds -74/Plant these in the fall. Takes 13 days to mature." #!String
    491: "Bok Choy Seeds/25/-300/Seeds -74/Plant these in the fall. Takes 4 days to mature." #!String
    492: "Yam Seeds/30/-300/Seeds -74/Plant these in the fall. Takes 10 days to mature." #!String
    493: "Cranberry Seeds/120/-300/Seeds -74/Plant these in the fall. Takes 7 days to mature, and continues to produce after first harvest." #!String
    494: "Beet Seeds/10/-300/Seeds -74/Plant these in the fall. Takes 6 days to mature." #!String
    495: "Spring Seeds/35/-300/Seeds -74/An assortment of wild spring seeds." #!String
    496: "Summer Seeds/55/-300/Seeds -74/An assortment of wild summer seeds." #!String
    497: "Fall Seeds/45/-300/Seeds -74/An assortment of wild fall seeds." #!String
    498: "Winter Seeds/30/-300/Seeds -74/An assortment of wild winter seeds." #!String
    499: "Ancient Seeds/30/-300/Seeds -74/Could these still grow?" #!String
    516: "Small Glow Ring/Emits a small, constant light./100/Ring" #!String
    517: "Glow Ring/Emits a constant light./200/Ring" #!String
    518: "Small Magnet Ring/Slightly increases your radius for collecting items./100/Ring" #!String
    519: "Magnet Ring/Increases your radius for collecting items./200/Ring" #!String
    520: "Slime Charmer Ring/Prevents damage from slimes./700/Ring" #!String
    521: "Warrior Ring/Occasionally infuses the wearer with \"warrior energy\" after slaying a monster./1500/Ring" #!String
    522: "Vampire Ring/Gain a little health every time you slay a monster./1500/Ring" #!String
    523: "Savage Ring/Gain a short speed boost whenever you slay a monster./1500/Ring" #!String
    524: "Ring of Yoba/Occasionally shields the wearer from damage./1500/Ring" #!String
    525: "Sturdy Ring/Cuts the duration of negative status effects in half./1500/Ring" #!String
    526: "Burglar's Ring/Monsters have a greater chance of dropping loot./1500/Ring" #!String
    527: "Iridium Band/Glows, attracts items, and increases attack damage by 10%./2000/Ring" #!String
    528: "Jukebox Ring/Plays a random assortment of music you've heard./200/Ring" #!String
    529: "Amethyst Ring/Increases knockback by 10%./200/Ring" #!String
    530: "Topaz Ring/Increases weapon precision by 10%./200/Ring" #!String
    531: "Aquamarine Ring/Increases critical strike chance by 10%./400/Ring" #!String
    532: "Jade Ring/Increases critical strike power by 10%./400/Ring" #!String
    533: "Emerald Ring/Increases weapon speed by 10%./600/Ring" #!String
    534: "Ruby Ring/Increases attack by 10%./600/Ring" #!String
    535: "Geode/50/-300/Basic/A blacksmith can break this open for you./538 542 548 549 552 555 556 557 558 566 568 569 571 574 576 121" #!String
    536: "Frozen Geode/100/-300/Basic/A blacksmith can break this open for you./541 544 545 546 550 551 559 560 561 564 567 572 573 577 123" #!String
    537: "Magma Geode/150/-300/Basic/A blacksmith can break this open for you./539 540 543 547 553 554 562 563 565 570 575 578 122" #!String
    538: "Alamite/150/-300/Minerals -12/Its distinctive fluorescence makes it a favorite among rock collectors." #!String
    539: "Bixite/300/-300/Minerals -12/A dark metallic Mineral sought after for its cubic structure." #!String
    540: "Baryte/50/-300/Minerals -12/The best specimens resemble a desert rose." #!String
    541: "Aerinite/125/-300/Minerals -12/These crystals are curiously light." #!String
    542: "Calcite/75/-300/Minerals -12/This yellow crystal is speckled with shimmering nodules." #!String
    543: "Dolomite/300/-300/Minerals -12/It can occur in coral reefs, often near an underwater volcano." #!String
    544: "Esperite/100/-300/Minerals -12/The crystals glow bright green when stimulated." #!String
    545: "Fluorapatite/200/-300/Minerals -12/Small amounts are found in human teeth." #!String
    546: "Geminite/150/-300/Minerals -12/Occurs in brilliant clusters." #!String
    547: "Helvite/450/-300/Minerals -12/It grows in a triangular column." #!String
    548: "Jamborite/150/-300/Minerals -12/The crystals are so tightly packed it almost looks fuzzy." #!String
    549: "Jagoite/115/-300/Minerals -12/A high volume of tiny crystals makes it very glittery." #!String
    550: "Kyanite/250/-300/Minerals -12/The geometric faces are as smooth as glass." #!String
    551: "Lunarite/200/-300/Minerals -12/The cratered white orbs form a tight cluster." #!String
    552: "Malachite/100/-300/Minerals -12/A popular ornamental stone, used in sculpture and to make green paint." #!String
    553: "Neptunite/400/-300/Minerals -12/A jet-black crystal that is unusually reflective." #!String
    554: "Lemon Stone/200/-300/Minerals -12/Some claim the powdered crystal is a dwarvish delicacy." #!String
    555: "Nekoite/80/-300/Minerals -12/The delicate shards form a tiny pink meadow." #!String
    556: "Orpiment/80/-300/Minerals -12/Despite its high toxicity, this Mineral is widely used in manufacturing and folk medicine." #!String
    557: "Petrified Slime/120/-300/Minerals -12/This little guy may be 100,000 years old." #!String
    558: "Thunder Egg/100/-300/Minerals -12/According to legend, angry thunder spirits would throw these stones at one another." #!String
    559: "Pyrite/120/-300/Minerals -12/Commonly known as \"Fool's Gold\"." #!String
    560: "Ocean Stone/220/-300/Minerals -12/An old legend claims these stones are the mosaics of ancient mermaids." #!String
    561: "Ghost Crystal/200/-300/Minerals -12/There is an aura of coldness around this crystal." #!String
    562: "Tigerseye/275/-300/Minerals -12/A stripe of shimmering gold gives this gem a warm luster." #!String
    563: "Jasper/150/-300/Minerals -12/When polished, this stone becomes attactively luminous. Prized by ancient peoples for thousands of years." #!String
    564: "Opal/150/-300/Minerals -12/Its internal structure causes it to reflect a rainbow of light." #!String
    565: "Fire Opal/350/-300/Minerals -12/A rare variety of opal, named for its red spots." #!String
    566: "Celestine/125/-300/Minerals -12/Some early life forms had bones made from this." #!String
    567: "Marble/110/-300/Minerals -12/A very popular material for sculptures and construction." #!String
    568: "Sandstone/60/-300/Minerals -12/A common type of stone with red and brown striations." #!String
    569: "Granite/75/-300/Minerals -12/A speckled Mineral that is commonly used in construction." #!String
    570: "Basalt/175/-300/Minerals -12/Forms near searing hot magma." #!String
    571: "Limestone/15/-300/Minerals -12/A very common type of stone. It's not worth very much." #!String
    572: "Soapstone/120/-300/Minerals -12/Because of its relatively soft consistency, this stone is very popular for carving." #!String
    573: "Hematite/150/-300/Minerals -12/An iron-based Mineral with interesting magnetic properties." #!String
    574: "Mudstone/25/-300/Minerals -12/A fine-grained rock made from ancient clay or mud." #!String
    575: "Obsidian/200/-300/Minerals -12/A volcanic glass that forms when lava cools rapidly." #!String
    576: "Slate/85/-300/Minerals -12/It's extremely resistant to water, making it a good roofing material." #!String
    577: "Fairy Stone/250/-300/Minerals -12/An old miner's song suggests these are made from the bones of ancient fairies." #!String
    578: "Star Shards/500/-300/Minerals -12/No one knows how these form. Some scientists claim that the microscopic structure displays unnatural regularity." #!String
    579: "Prehistoric Scapula/100/-300/Arch/Commonly known as a \"shoulder blade\"... It's unclear what species it belonged to./Item 1 289/Town .01" #!String
    580: "Prehistoric Tibia/100/-300/Arch/A thick and sturdy leg bone./Item 1 289/Forest .01" #!String
    581: "Prehistoric Skull/100/-300/Arch/This is definitely a mammalian skull./Item 1 289/Mountain .01" #!String
    582: "Skeletal Hand/100/-300/Arch/It's a wonder all these ancient little pieces lasted so long./Item 1 289/Beach .01" #!String
    583: "Prehistoric Rib/100/-300/Arch/Little gouge marks on the side suggest that this rib was someone's dinner./Item 1 289/Farm .01" #!String
    584: "Prehistoric Vertebra/100/-300/Arch/A segment of some prehistoric creature's spine./Item 1 289/BusStop .01" #!String
    585: "Skeletal Tail/100/-300/Arch/It's pretty short for a tail./Item 1 289/UndergroundMine .01" #!String
    586: "Nautilus Fossil/80/-300/Arch/This must've washed up ages ago from an ancient coral reef. /Item 1 289/Beach .03" #!String
    587: "Amphibian Fossil/150/-300/Arch/The relatively short hind legs suggest some kind of primordial toad./Item 1 289/Forest .01 Mountain .01" #!String
    588: "Palm Fossil/100/-300/Arch/Palm Fossils are relatively common, but this happens to be a particularly well-preserved specimen./Item 1 289/Desert .1 Beach .01 Forest .01" #!String
    589: "Trilobite/50/-300/Arch/A long extinct relative of the crab./Item 1 289/Beach .03 Mountain .03 Forest .03" #!String
    590: "Artifact Spot/0/-300/asdf/Uh... how did you get this in your inventory? Ape made a booboo./Item 1 289/Beach .03 Mountain .03 Forest .03" #!String
    591: "Tulip/30/18/Basic -80/The most popular spring flower. Has a very faint sweet smell." #!String
    593: "Summer Spangle/90/18/Basic -80/A tropical bloom that thrives in the humid summer air. Has a sweet, tangy aroma." #!String
    595: "Fairy Rose/290/18/Basic -80/An old folk legend suggests that the sweet smell of this flower attracts fairies." #!String
    597: "Blue Jazz/50/18/Basic -80/The flower grows in a sphere to invite as many butterflies as possible." #!String
    599: "Sprinkler/100/-300/Crafting -8/Waters the 4 adjacent tiles every morning." #!String
    604: "Plum Pudding/260/70/Cooking -7/A traditional holiday treat./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    605: "Artichoke Dip/210/40/Cooking -7/It's cool and refreshing./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    606: "Stir Fry/335/80/Cooking -7/Julienned vegetables on a bed of rice./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    607: "Roasted Hazelnuts/270/70/Cooking -7/The roasting process creates a rich forest flavor./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    608: "Pumpkin Pie/385/90/Cooking -7/Silky pumpkin cream in a flakey crust./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    609: "Radish Salad/300/80/Cooking -7/The radishes are so crisp!/food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    610: "Fruit Salad/450/105/Cooking -7/A delicious combination of summer fruits./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    611: "Blackberry Cobbler/260/70/Cooking -7/There's nothing quite like it./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    612: "Cranberry Candy/175/50/Cooking -7/It's sweet enough to mask the bitter fruit./drink/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    613: "Apple/100/15/Basic -79/A crisp fruit used for juice and cider." #!String
    618: "Bruschetta/210/45/Cooking -7/Roasted tomatoes on a crisp white bread./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    621: "Quality Sprinkler/450/-300/Crafting -8/Waters the 8 adjacent tiles every morning." #!String
    628: "Cherry Sapling/850/-300/Basic -74/Takes 28 days to produce a mature cherry tree. Bears fruit in the spring. Only grows if the 8 surrounding \"tiles\" are empty." #!String
    629: "Apricot Sapling/500/-300/Basic -74/Takes 28 days to produce a mature Apricot tree. Bears fruit in the spring. Only grows if the 8 surrounding \"tiles\" are empty." #!String
    630: "Orange Sapling/1000/-300/Basic -74/Takes 28 days to produce a mature Orange tree. Bears fruit in the summer. Only grows if the 8 surrounding \"tiles\" are empty." #!String
    631: "Peach Sapling/1500/-300/Basic -74/Takes 28 days to produce a mature Peach tree. Bears fruit in the summer. Only grows if the 8 surrounding \"tiles\" are empty." #!String
    632: "Pomegranate Sapling/1500/-300/Basic -74/Takes 28 days to produce a mature Pomegranate tree. Bears fruit in the fall. Only grows if the 8 surrounding \"tiles\" are empty." #!String
    633: "Apple Sapling/1000/-300/Basic -74/Takes 28 days to produce a mature Apple tree. Bears fruit in the fall. Only grows if the 8 surrounding \"tiles\" are empty." #!String
    634: "Apricot/50/15/Basic -79/A tender little fruit with a rock-hard pit." #!String
    635: "Orange/100/15/Basic -79/Juicy, tangy, and bursting with sweet summer aroma." #!String
    636: "Peach/140/15/Basic -79/It's almost fuzzy to the touch." #!String
    637: "Pomegranate/140/15/Basic -79/Within the fruit are clusters of juicy seeds." #!String
    638: "Cherry/80/15/Basic -79/It's popular, and ripens sooner than most other fruits." #!String
    645: "Iridium Sprinkler/1000/-300/Crafting -8/Waters the 24 adjacent tiles every morning." #!String
    648: "Coleslaw/345/85/Cooking -7/It's light, fresh and very healthy./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    649: "Fiddlehead Risotto/350/90/Cooking -7/A creamy rice dish served with sauteed fern heads. It's a little bland./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    651: "Poppyseed Muffin/250/60/Cooking -7/It has a soothing effect./food/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    668: "Stone/0/15/Basic/There's stone ore in this stone." #!String
    670: "Stone/0/15/Basic/There's stone ore in this stone." #!String
    674: "Weeds/0/15/Basic/Ugly weeds." #!String
    675: "Weeds/0/15/Basic/Ugly weeds." #!String
    676: "Weeds/0/15/Basic/Ugly weeds." #!String
    677: "Weeds/0/15/Basic/Ugly weeds." #!String
    678: "Weeds/0/15/Basic/Ugly weeds." #!String
    679: "Weeds/0/15/Basic/Ugly weeds." #!String
    680: "Green Slime Egg/1000/-300/Basic/Can be hatched in a slime incubator." #!String
    681: "Rain Totem/20/-300/Crafting/Activate to greatly increase the chance for rain tomorrow. Consumed on use." #!String
    682: "Mutant Carp/1000/10/Fish -4/The strange waters of the sewer turned this carp into a monstrosity./Day^Spring Summer" #!String
    684: "Bug Meat/8/-300/Basic -28/It's a juicy wad of bug flesh." #!String
    685: "Bait/1/-300/Basic -21/Causes fish to bite faster. Must first be attached to a fishing rod." #!String
    686: "Spinner/250/-300/Basic -22/The shape makes it spin around in the water. Slightly increases the bite-rate when fishing." #!String
    687: "Dressed Spinner/500/-300/Basic -22/The metal tab and colorful streamers create an enticing spectacle for fish. Increases the bite-rate when fishing." #!String
    688: "Warp Totem: Farm/20/-300/Crafting/Warp directly to your house. Consumed on use." #!String
    689: "Warp Totem: Mountains/20/-300/Crafting/Warp directly to the mountains. Consumed on use." #!String
    690: "Warp Totem: Beach/20/-300/Crafting/Warp directly to the beach. Consumed on use." #!String
    691: "Barbed Hook/500/-300/Basic -22/Makes your catch more secure, causing the \"fishing bar\" to cling to your catch. Works best on slow, weak fish." #!String
    692: "Lead Bobber/150/-300/Basic -22/Adds weight to your \"fishing bar\", preventing it from bouncing along the bottom." #!String
    693: "Treasure Hunter/250/-300/Basic -22/Fish don't escape while collecting treasures. Also slightly increases the chance to find treasures." #!String
    694: "Trap Bobber/200/-300/Basic -22/Causes fish to escape slower when you aren't reeling them in." #!String
    695: "Cork Bobber/250/-300/Basic -22/Slightly increases the size of your \"fishing bar\"." #!String
    698: "Sturgeon/200/10/Fish -4/An ancient bottom-feeder with a dwindling population. Females can live up to 150 years./Day^Spring Summer" #!String
    699: "Tiger Trout/150/10/Fish -4/A rare hybrid trout that cannot bear offspring of its own./Day^Spring Summer" #!String
    700: "Bullhead/75/10/Fish -4/A relative of the catfish that eats a variety of foods off the lake bottom./Day^Spring Summer" #!String
    701: "Tilapia/75/10/Fish -4/A primarily vegetarian fish that prefers warm water./Day^Spring Summer" #!String
    702: "Chub/50/10/Fish -4/A common freshwater fish known for its voracious appetite./Day^Spring Summer" #!String
    703: "Magnet/15/-300/Basic -21/Increases the chance of finding treasures when fishing. However, fish aren't crazy about the taste." #!String
    704: "Dorado/100/10/Fish -4/A fierce carnivore with brilliant orange scales./Day^Summer" #!String
    705: "Albacore/75/10/Fish -4/Prefers temperature \"edges\" where cool and warm water meet./Day^Spring Fall" #!String
    706: "Shad/60/10/Fish -4/Lives in a school at sea, but returns to the rivers to spawn./Day^Spring Summer Fall" #!String
    707: "Lingcod/120/10/Fish -4/A fearsome predator that will eat almost anything it can cram into its mouth./Day^Fall" #!String
    708: "Halibut/80/10/Fish -4/A flat fish that lives on the ocean floor./Day^Spring Summer" #!String
    709: "Hardwood/15/-300/Basic -16/A special kind of wood with superior strength and beauty." #!String
    710: "Crab Pot/50/-300/Crafting/Place it in the water, load it with bait, and check the next day to see if you've caught anything. Works in streams, lakes, and the ocean." #!String
    715: "Lobster/120/-300/Fish -4/A large ocean-dwelling crustacean with a strong tail./Day^Spring Summer" #!String
    716: "Crayfish/75/-300/Fish -4/A small freshwater relative of the lobster./Day^Spring Summer" #!String
    717: "Crab/100/-300/Fish -4/A marine crustacean with two powerful pincers./Day^Spring Summer" #!String
    718: "Cockle/50/-300/Fish -4/A common saltwater clam./Day^Spring Summer" #!String
    719: "Mussel/30/-300/Fish -4/A common bivalve that often lives in clusters./Day^Spring Summer" #!String
    720: "Shrimp/60/-300/Fish -4/A scavenger that feeds off the ocean floor. Widely prized for its meat./Day^Spring Summer" #!String
    721: "Snail/65/-300/Fish -4/A wide-ranging mollusc that lives in a spiral shell./Day^Spring Summer" #!String
    722: "Periwinkle/20/-300/Fish -4/A tiny freshwater snail that lives in a blue shell./Day^Spring Summer" #!String
    723: "Oyster/40/-300/Fish -4/Constantly filters water to find food. In the process, it removes dangerous toxins from the environment./Day^Spring Summer" #!String
    724: "Maple Syrup/200/20/Basic -27/A sweet syrup with a unique flavor./drink/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    725: "Oak Resin/150/-300/Basic -27/A sticky, fragrant substance derived from oak sap." #!String
    726: "Pine Tar/100/-300/Basic -27/A pungent substance derived from pine sap." #!String
    727: "Chowder/135/90/Cooking -7/A perfect way to warm yourself after a cold night at sea./food/0 1 0 0 0 0 0 0 0 0 0/1440" #!String
    728: "Fish Stew/175/90/Cooking -7/It smells a lot like the sea. Tastes better, though./food/0 3 0 0 0 0 0 0 0 0 0/1440" #!String
    729: "Escargot/125/90/Cooking -7/Butter-soaked snails cooked to perfection./food/0 2 0 0 0 0 0 0 0 0 0/1440" #!String
    730: "Lobster Bisque/205/90/Cooking -7/This delicate soup is a secret family recipe of Willy's./food/0 3 0 0 0 0 0 50 0 0 0/1440" #!String
    731: "Maple Bar/300/90/Cooking -7/It's a sweet doughnut topped with a rich maple glaze./food/1 1 1 0 0 0 0 0 0 0 0/1440" #!String
    732: "Crab Cakes/275/90/Cooking -7/Crab, bread crumbs, and egg formed into patties then fried to a golden brown./food/0 0 0 0 0 0 0 0 0 1 1/1440" #!String
    734: "Woodskip/75/10/Fish -4/A very sensitive fish that can only live in pools deep in the forest./Day^Spring Summer" #!String
    745: "Strawberry Seeds/0/-300/Seeds -74/Plant these in spring. Takes 8 days to mature, and keeps producing strawberries after that." #!String
    746: "Jack-O-Lantern/0/-300/Crafting -8/A whimsical fall decoration." #!String
    747: "Rotten Plant/0/-300/Basic -20/Decomposing organic material. It's slimy and unpleasant." #!String
    748: "Rotten Plant/0/-300/Basic -20/Decomposing organic material. It's slimy and unpleasant." #!String
    749: "Omni Geode/0/-300/Basic/A blacksmith can break this open for you. These geodes contain a wide variety of Minerals./538 542 548 549 552 555 556 557 558 566 568 569 571 574 576 541 544 545 546 550 551 559 560 561 564 567 572 573 577 539 540 543 547 553 554 562 563 565 570 575 578 121 122 123" #!String
    750: "Weeds/0/15/Basic/Ugly weeds." #!String
    751: "Stone/0/15/Basic/There's copper ore in this stone." #!String
    760: "Stone/0/15/Basic/.." #!String
    762: "Stone/0/15/Basic/.." #!String
    764: "Stone/0/15/Basic/gold ore" #!String
    765: "Stone/0/15/Basic/iridium ore" #!String
    766: "Slime/5/-300/Basic -28/A shimmering, gelatinous glob with no smell." #!String
    767: "Bat Wing/15/-300/Basic -28/The material is surprisingly delicate." #!String
    768: "Solar Essence/40/-300/Basic -28/The glowing face is warm to the touch." #!String
    769: "Void Essence/50/-300/Basic -28/It's quivering with dark energy." #!String
    770: "Mixed Seeds/0/-300/Seeds -74/There's a little bit of everything here. Plant them and see what grows!" #!String
    771: "Fiber/1/-300/Basic -16/Raw material sourced from plants." #!String
    772: "Oil of Garlic/1000/80/Cooking -7/Drink this and weaker monsters will avoid you./drink/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    773: "Life Elixir/500/80/Cooking -7/Restores health to full./drink/0 0 0 0 0 0 0 0 0 0 0/0" #!String
    774: "Wild Bait/15/-300/Basic -21/A unique recipe from Linus. It appeals to all fish." #!String
    775: "Glacierfish/1000/10/Fish -4/Builds a nest on the underside of glaciers./Day^Winter" #!String
    784: "Weeds/0/15/Basic/Ugly weeds." #!String
    785: "Weeds/0/15/Basic/Ugly weeds." #!String
    786: "Weeds/0/15/Basic/Ugly weeds." #!String
    787: "Battery Pack/500/-300/Basic -16/It's fully charged with precious energy." #!String
    788: "Lost Axe/0/-300/Quest/Robin's been looking everywhere for it." #!String
    789: "Lucky Purple Shorts/0/-300/Quest/Better not inspect these too closely." #!String
    790: "Berry Basket/0/-300/Quest/The fibers are stained with berry juice." #!String
    792: "Weeds/0/15/Basic/Ugly weeds." #!String
    793: "Weeds/0/15/Basic/Ugly weeds." #!String
    794: "Weeds/0/15/Basic/Ugly weeds." #!String
    795: "Void Salmon/150/25/Fish -4/A salmon, twisted by void energy. The fresh meat is jet black, but rapidly turns pink when exposed to air./Day^Spring Summer" #!String
    796: "Slimejack/100/15/Fish -4/He's coated in a very thick layer of slime. He keeps slipping out of your hands!/Day^Spring Summer" #!String
```

### Format

#### Rings
Rings (indexes 516–534 or `Ring.ringLowerIndexRange` through `Ring.ringUpperIndexRange`) are
parsed by the `Ring` constructor and contain four fields:

index | field                   | example value
:---- |:----------------------- |:-------------
0     | name                    | _Burglar's Ring_
1     | description             | _Monsters have a greater chance of dropping loot._
2     | price<br /><small>(if sold by player)</small> | _1500_
3     | type<br /><small>(always "Ring")</small> | _Ring_

Rings have a hardcoded edibility of -300 (inedible) and category -96 (`Object.ringCategory`).

#### Other objects
All other objects contain at least five fields:

index | field                   | example value
:---- |:----------------------- |:-------------
0     | name                    | _Glacierfish_
1     | price<br /><small>(if sold by player)</small> | _1000_
2     | edibility               | _10_
3     | type and category       | _Fish -4_
4     | description             | _Builds a nest on the underside of glaciers._

Some entries have more fields, but those don't seem to be used (needs to be investigated further).

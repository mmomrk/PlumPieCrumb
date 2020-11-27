# PlumPieCrumb
A recipe for making a plum pie with crumb top


## Ingredients, import, var
```DeLaCuisine

assert this.kitchen is basic, "You will need at least a basic kitchen to be able to run the recipe"

butter = Butter( 130g )
sugar = Sugar( 205g )
milk = Milk( 125ml )
eggs = Eggs( 2 )
flour = Flour( 250g )
plumes = deSeed(Plumes( 650g ))
bPowder = BakingPowder( 1teaspoon )
salt = Salt( 1./4teaspoon )
cinnamon = ( Cinnamon or Vanilla ) ( 3spoons )

var mixer = Mixer() or Hands().grab(Spoon())
var oil = SunflowerOil() or OliveOil()
var dish = BakingDish().line( Foil(ALUMINIUM) ).cover(oil).cover(Flour)

assert dish.surface == 6dm +- 15%, "Scale your ingredients. Tested on the 30x20cm baking glass dish. Comment this line at your own risk"  // Mmm, syntactic sugar...  //TODO: refactor this line and add proper initialisation to the constructor
assert dish.sideWalls is covered, "Cover the sidewalls. The pie will stick to it!"
assert dish.sideWalls is covered, "Cover the sidewalls. The pie will stick to it!"  // This step is really important
assert butter() is TASTY, "Don't bother trying to implement it if you cannot claim and prove that the butter IS good"
assert all( p is JUICY for p in plumes() ), "Don't bother trying this recipe with dry non-juicy plumes. Thank me later for saving your time"
```
## Part 1: Bottom layer
```DeLaCuisine
st1 = mix( sugar(125g) + eggs(2) + salt() + cinnamon() )
st2 = mix( st1 + melt(butter(50g /*!Not all of it!*/)) + milk() + flour(), mixer) // Check Kitchen.Basic.melt documentation at the delacuisine.code
dish.add(st2)
dish.flatten()
```
## Part 2: The filling
```DeLaCuisine
plumes= p.slice(1) for p in plumes()  // Cut once. Split into two halves
dish.add(plumes())
dish.equaliseHeight() // Do not cunfuse with flatten()
if ( p.sweetness for p in plumes() ).average() < this.eater.preference.sweet: // This line also demonstrates the power of LangueDLC 
  dish.add( Sugar(1spoon) )
  if ( p.sweetness for p in plumes() ).average() + Sugar(1spoon).sweetness < this.eater.preference.sweet: // This line also demonstrates the power of LangueDLC // This line also demonstrates the lazyness of ProgrammeurDLC
    dish.add( Sugar(1spoon) )
```

## Part 3: The top layer, Streusel
```DeLaCuisine
assert butter.temperature < 10C, "Freeze! You will not make a streusel with a warm butter. Loose 20 minutes"
bowl = MixingBowl()
while bowl.contents > Plume.seed.size():
  m1 = mix( flour(100g) + sugar(80g) + butter(80g), knife, length=STEP)
while bowl.contents > Sunflower.seed.size():
  m1 = mix( flour(100g) + sugar(80g) + butter(80g), Hands)
assert bowl.contents.look == Parmesane.grated(FINE).look \
  and  bowl.contents.look == Parmesane.grated(FINE).look, \
  "Don't be fooled by the look. It's no the proper Streusel. Redo"
```
## Part 4: Grande Finale
```DeLaCuisine
dish.add(bowl.contents())
dish.equaliseHeight()
stove = Stove(minT=180C, maxT=200C)
stove.add(dish)
stove.letBake(50min, maxT=55min, guaranteedT=40min, recheckT=5min, noseBakingSensor=ON, finishWhen=Baker.Standard.FinishCriterionsDefault)
// Some prefer the cake when it is cooled to the room temperature

// Remove when the check is added to the stable version:
this._Preprocessor_.checkVarUtilisation() // It will be added to the compile-time in the future revisions
```
WARNING: Please don't post compiler-related bugs to this repo
DISCLAIMER: MIT License. Do it at your own risk

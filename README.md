# Cobbleland Datapack

 # How to add textures to a PolymerItem
 
### Example on adding the Dynamax Candy
Let's first assume `MOD_ID` is equal to `cobbletransformations`<br>
We need to declare a PolymerModelData we will use later.<br>
In the main class of the mod (the one with the `initialize()` method) let's declare 
`lateinit var candyModelData: PolymerModelData` as well as the item itself 
`val DYNAMAX_CANDY: DynamaxCandy = DynamaxCandy(FabricItemSettings().maxCount(64).rarity(Rarity.RARE), Items.HONEYCOMB)`

Then, in the `initialize()` method, we have to register the custom item 
`Registry.register(Registries.ITEM, Identifier(MOD_ID, "dynamaxcandy"), DYNAMAX_CANDY)`<br>
Then we have to check if the mod is valid `val isModValid = PolymerResourcePackUtils.addModAssets(MOD_ID)` (will return a boolean)
<br>Now let's mark the resourcepack as required and request the model of the item
```kotlin
if(isModValid){
    PolymerResourcePackUtils.markAsRequired()
    candyModelData = PolymerResourcePackUtils.requestModel(Items.HONEYCOMB, Identifier(MOD_ID, 
        "item/dynamaxcandy"))
        }
```

Then, in the custom item's class (`DynamaxCandy` in this case), let's declare a PolymerModelData object `PolymerModelData modelData;`
<br>Then we have to override the `getPolymerCustomModelData()` method
```java
@Override
    public int getPolymerCustomModelData(ItemStack itemStack, @Nullable ServerPlayerEntity player){
        this.modelData = cobbletransformations.candyModelData;
        return this.modelData.value();
    }
```

Then, in the `resources/assets` folder, let's create a new folder called exactly like the `MOD_ID` (`cobbletransformations`).
<br>Inside of it, let's create 3 folders called `lang`, `models` and `textures`

In the `lang` folder, let's create a file called `en_us.json` and inside of it, we will have to give the displayed name of the item
```json5
{
  "item.cobbletransformations.dynamaxcandy": "Dynamax Candy"
}
```

In the `models` folder, let's create a folder called `item`, and inside of it, we have to create a json file called 
exactly as the item name
(in this case `dynamaxcandy.json`), and inside of it let's declare the `parent` and `textures`
```json5
{
  "parent": "item/generated",
  "textures": {
    "layer0": "cobbletransformations:item/dynamaxcandy"
  }
}
```

Finally, in the `textures` folder, let's create a new folder called `item`, and inside of it let's insert a .png file 
of size 16x16 with the item's textures, and name it as the item's name (in this case `dynamaxcandy.png`)


### Add the files to the Resource Pack
After compiling the mod, we will have to recreate the same exact structure of the `assets` folder inside the resource pack.
<br>So the resource pack will now have an `assets` folder, with the `lang`, `models` and `textures` 
folders and their respective files inside, as done for the mod itself
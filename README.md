# Discord.js-MongoDb-Economy
Do you also want to create an economy system in discord.js v14?
Well then this tutorial is for you.

First of all you need an command handler which supports mongoose.
https://github.com/E1NZ1/Discord.js-SlashCommand-Handler
This is the best handler so use it for best experience.

# Getting Started
### Ok so First let's create an schema
Create an folder models and make an file `eco.js`.

Then paste the following code there.
```js
const mongoose = require("mongoose");

const eco = mongoose.Schema({
    userid: { type: String },
    cash: { type: Number, default: 100 }, // Default is optional.
})

module.exports = mongoose.model("eco", eco)
```

### Useful Information (Required to Know)
Good. Now your main thing is ready here is a few functions to use in the commands

```js
// we will define data in the code given late
data.cash += 100; // add some cash
data.cash -= 100; // remove cash
data.cash = 100: // set Cash
await data.save();
```

# Creating Balamce Command
### Ok so let's create an command
--- 
```js
// Balance Command
const { EmbedBuilder } = require("discord.js")
const eco = require("../../models/eco");

module.exports = {
    name: "balance",
    description: "see your fazcash",
    options: [
        {
            name: "user",
            description: "user to view cash of",
            type: 6,
        },
    ],
    run: async (client, interaction) => {
        const user = interaction.options.getUser("user") || interaction.user;
        const data =
              (await eco.findOne({ userid: user.id })) ||
              (await eco.create({ userid: user.id }));
        
        await interaction.reply({
            embeds: [
                new EmbedBuilder()
               .setDescription(`${user.tag} currently has ${data.cash} cash`)
                .setColor("#303136")
                ],
        })
    }
}
```
Wonderful. Now try creating your own commands with the tips i gave

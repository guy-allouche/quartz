### Inverting who rolls
Using [[Rolling Dice#Variant Defense Rolls|the Defense Rolls variant rule]], players roll the dice when attacking as normal, but also when they are attacked. We'd like for the underlying bonuses and calculations to be symmetrical, so we know it works out the same with the non-variant rule (attacker always rolls). It turns out we can do this relatively elegantly, at least with DnD 2's attack resolution mechanics.

When a player attacks (the regular attacker rolls case), they roll 2d6 and add some attack bonus. This is reduced by the target's defense bonus, and the total is the damage they take. So the damage on an attack is:
`(2d6 + ATK) - DEF`

When a player is attacked, we invert who rolls the dice, so the player rolls 2d6, adds their defense bonus, and reduces the total from the attack's static damage. We're looking for a magical static damage number `X` that we can add to the normal attack bonus to form the attack's static damage; `X` should be chosen so that the damage distribution is exactly the same as if the attacker had rolled the dice. So we are trying to solve
`(2d6 + ATK) - DEF = X + ATK - (2d6 + DEF)`
Which trivially reduces to
`2d6 = X - 2d6`

Remember, `2d6` is a distribution, so we are trying to choose an `X`  such that `X - 2d6` is the exact same distribution as `2d6`. 
The key to make this possible is that the `2d6` distribution is *symmetric around its mean*, 7. The chance of getting a total of 6 is the same as a total of 8, likewise for 5 and 9, 4 and 10, etc. You can intuit this symmetry by looking at the edge cases - there's only one combination for a total of 12 (double 6's), and only one combination for a total of 2 (snake eyes). There are two combinations for 3 (1,2 or 2,1), and likewise for 11 (5,6 or 6,5). Finally, notice that all these pairs add up to 14.

Now the `X` we must choose becomes clear. If `X=14`, our new distribution is `14-2d6`. This maps a result of 2 on the `2d6` to 12, 3 to 11, ..., and 12 back to 2. Each of these pairs have the same probability, so the final distribution is the same one we started with! All that is to say,
`2d6 = 14 - 2d6` (!)

So, to have defenders roll the dice without impacting the math, simply add 14 to the attacker's attack bonus and make this the static pre-mitigation damage. It ends up equivalent to the attacker rolling the dice.
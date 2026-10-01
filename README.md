# game
// --- Monster Battle Game ---
const game = {
    playerHp: 100,
    maxPlayerHp: 100,
    monsterHp: 80,
    maxMonsterHp: 80,
    potions: 3,

    status() {
        console.log(`%c--- BATTLE STATUS ---`, "font-weight: bold; color: #333;");
        console.log(`❤️ Your HP: ${this.playerHp}/${this.maxPlayerHp} | 🧪 Potions left: ${this.potions}`);
        console.log(`👹 Monster's HP: ${this.monsterHp}/${this.maxMonsterHp}`);
        console.log(`---------------------`);
    },

    attack() {
        if (this.playerHp <= 0 || this.monsterHp <= 0) {
            console.log("The battle is over! Refresh the page or re-run the script to play again.");
            return;
        }

        // Player attack
        const playerDamage = Math.floor(Math.random() * 15) + 10;
        this.monsterHp = Math.max(0, this.monsterHp - playerDamage);
        console.log(`%c⚔️ You strike the monster for ${playerDamage} damage!`, "color: #4CAF50; font-weight: bold;");

        // Check if monster died
        if (this.monsterHp === 0) {
            console.log(`%c🏆 VICTORY! You defeated the monster! 🎉`, "font-size: 14px; font-weight: bold; color: #FF9800;");
            return;
        }

        // Monster counterattack
        this.monsterTurn();
    },

    heal() {
        if (this.playerHp <= 0 || this.monsterHp <= 0) {
            console.log("The battle is over!");
            return;
        }

        if (this.potions <= 0) {
            console.log(`%c⚠️ You are out of health potions!`, "color: #E91E63; font-weight: bold;");
            return;
        }

        this.potions--;
        const healAmount = 25;
        this.playerHp = Math.min(this.maxPlayerHp, this.playerHp + healAmount);
        console.log(`%c🧪 You drank a potion and recovered ${healAmount} HP!`, "color: #2196F3; font-weight: bold;");

        // Monster counterattack
        this.monsterTurn();
    },

    monsterTurn() {
        const monsterDamage = Math.floor(Math.random() * 18) + 5;
        this.playerHp = Math.max(0, this.playerHp - monsterDamage);
        console.log(`%c👹 The monster hits you back for ${monsterDamage} damage!`, "color: #F44336; font-weight: bold;");

        if (this.playerHp === 0) {
            console.log(`%c💀 DEFEAT! You were slain by the monster... ☠️`, "font-size: 14px; font-weight: bold; color: #F44336;");
            return;
        }

        this.status();
    }
};

// Welcome message
console.log("%c⚔️ WILD MONSTER APPEARED! ⚔️️", "font-size: 16px; font-weight: bold; color: #9C27B0;");
console.log("Commands you can use:");
console.log("  %cgame.attack()%c - Attack the monster", "font-weight: bold; color: #4CAF50;", "");
console.log("  %cgame.heal()%c   - Drink a health potion", "font-weight: bold; color: #2196F3;", "");
console.log("  %cgame.status()%c - Check current stats", "font-weight: bold; color: #333;", "");
game.status();

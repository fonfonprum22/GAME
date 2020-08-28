<template>
  <div class="container">
    <div class="row">
      <div class="col">
        <button type="button" class="btn btn-outline-primary" v-on:click="created()">Start</button>
      </div>
    </div>
    <div class="row">
      <div class="col-sm">
        <div class="card text-center">
          <div class="card-header">Hero {{unitHero.name}}</div>
          <div class="card-body">
            <img
              :style="{height:unitHero.percent + 'px'}"
              :src="require(`../assets/Player/${unitHero.url}`)"
              class="img-fluid"
              alt="Responsive image"
            />
          </div>
          <div class="card-footer text-muted">
            HP {{unitHero.hp}}
            <div class="progress">
              <div
                class="progress-bar"
                role="progressbar"
                :style="{width:unitHero.percent + '%'}"
                aria-valuenow="25"
                aria-valuemin="0"
                aria-valuemax="100"
              >{{unitHero.percent}}%</div>
            </div>
          </div>
        </div>
      </div>

      <div class="col-sm">
        <div class="card text-center">
          <div class="card-header">Monster {{unitMonster.name}}</div>
          <div class="card-body">
            <img
              :style="{height:unitMonster.percent + 'px'}"
              :src="require(`../assets/Monster/${unitMonster.url}`)"
              class="img-fluid"
              alt="Responsive image"
            />
          </div>
          <div class="card-footer text-muted">
            HP {{unitMonster.hp}}
            <div class="progress">
              <div
                class="progress-bar"
                role="progressbar"
                :style="{width:unitMonster.percent + '%'}"
                aria-valuenow="25"
                aria-valuemin="0"
                aria-valuemax="100"
              >{{unitMonster.percent}}%</div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="row">
      <div class="col" v-if="gameEnd==false">
        <button  type="button" class="btn btn-outline-primary" v-on:click="attack(3,10),monattack(3,5)">Attack</button>
        <button
          type="button"
          class="btn btn-outline-primary"
          v-on:click="attack(5,15),monattack(4,10)"
        >Special Attack</button>
      </div>
      <div class="col" v-if="gameEnd==true && win==true">
        <img
              
              :src="require(`../assets/Player/${unitHero.url}`)"
              class="img-fluid"
              alt="Responsive image"
            />
            Win!


     
    </div>
    <div class="col" v-if="gameEnd==true && win==false">
       <img
              
              :src="require(`../assets/Monster/${unitMonster.url}`)"
              class="img-fluid"
              alt="Responsive image"
            />
            Win!


     
    </div>
  </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      unitHero: {},
      unitMonster: {},
      Hero: [
        { name: "Anakin Skywalker",hpmax:100,hp: 100, url: "Anakin.png","percent":100},
        { name: " Doraemon ",hpmax:200,hp: 200, url: "Doraemon.jpg","percent":100},
        { name: " Iron man",hpmax:150, hp: 150, url: "IronMan.png","percent":100 },
      ],
      Monster: [
        { name: "Thanos",hpmax:150, hp: 150, url: "Thanos.jpg","percent":100},
        { name: "Darth  vader",hpmax:180, hp: 180, url: "DarthVader.jpg","percent":100},
        { name: "Cell ",hpmax:300, hp: 300, url: "cell.jpg","percent":100 },
      ],
      gameEnd:false,
      win:true
    };
  },

  methods: {
    attack: function (min, max) {
      let dmg = Math.max(Math.floor(Math.random() * max) + 1, min);
      this.unitMonster.hp = this.unitMonster.hp - dmg;
      if (this.unitMonster.hp<=0){
        this.unitMonster.hp=0
        this.gameEnd=true
        this.win=true
      }
      this.unitMonster.percent = this.unitMonster.hp *100/this.unitMonster.hpmax
    },
     monattack: function (min, max) {
      let mondmg = Math.max(Math.floor(Math.random() * max) + 1, min);
      this.unitHero.hp = this.unitHero.hp - mondmg;
      if (this.unitHero.hp<=0){
        this.unitHero.hp=0
        this.gameEnd=true
        this.win=false
      }
      this.unitHero.percent = this.unitHero.hp *100/this.unitHero.hpmax
    },
    created: function() {
    this.unitHero = this.Hero[Math.max(Math.floor(Math.random() * 2) + 1, 0)];
    this.unitMonster = this.Monster[
      Math.max(Math.floor(Math.random() * 2) + 1, 0)
    ];
  },
  },
  created() {
    this.unitHero = this.Hero[Math.max(Math.floor(Math.random() * 2) + 1, 0)];
    this.unitMonster = this.Monster[
      Math.max(Math.floor(Math.random() * 2) + 1, 0)
    ];
  },
 

};
</script>

<style>
</style>
<template>
  <div class="about">
    <h1>Appli créée en suivant le tuto:</h1>
    <a
      href="https://www.udemy.com/course/vue-3-par-la-pratique/"
      target="_blank"
      >https://www.udemy.com/course/vue-3-par-la-pratique/</a
    >
  </div>
  <div class="modif">
    <div class="bold">Modifications et remarques</div>
    <ul>
      <li>
        Les noms des composants doivent être au format
        <span class="termes">MyForm</span> au lieu de
        <span class="termes">Form</span>
        dans le tuto, par exemple.
        <a
          target="_blank"
          href="https://vue3-fr.netlify.app/style-guide/#la-casse-des-noms-de-composants-fortement-recommandee"
          >https://vue3-fr.netlify.app/style-guide/#la-casse-des-noms-de-composants-fortement-recommandee</a
        >
      </li>
      <li><span class="astuces">maj+alt+f</span> pour reformater le code</li>
      <li>
        Si maj/alt/f ne suffit pas et problèmes avec eslint prettier ne
        disparaissent pas, faire dans le terminal
        <span class="codes">yarn run lint --fix</span>
      </li>
      <li>
        Astuce (apprise lors du tuto, ben oui je ne la connaissais pas, ne vous
        moquez pas!): lorsqu'on sélectionne un terme si on fait
        <span class="astuces">ctrl+d</span> le suivant identique est également
        sélectionné (possible de le faire plusieurs fois).
      </li>
      <li>
        Section 7 "persister dans le localStorage" remettre le bout de code que
        le formateur a enlevé car ne semblait plus rien faire car perso sans ce
        code j'ai des erreurs dans la console: dans services/tasks fonction
        create <span class="codes">if (tasks === null) { tasks = []; }</span>
      </li>
      <li>
        Déploiement sur netlify: si on ne ferme pas l'onglet du navigateur même
        en raffraîchissant on ne voit pas les modifications.
      </li>
    </ul>
  </div>
</template>
<style scoped>
.bold {
  font-size: 2rem;
  font-weight: bolder;
  color: red;
  text-align: center;
}
.modif {
  margin: 3rem auto;
  color: rgb(209, 33, 33);
  font-size: 1.3rem;
  text-align: left;
}
li {
  margin: 1rem auto;
}
.termes {
  font-weight: bolder;
}
.astuces {
  color: blue;
  font-weight: bolder;
}
.codes {
  color: #42b983;
  font-weight: bolder;
  font-style: italic;
}
li a {
  font-size: 0.8rem;
  color: rgb(110, 152, 192);
}
</style>

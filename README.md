# exo_20220126.md
Devoir Wikidata - Rodin

Voici la requête wikidata permettant de faire afficher sur une carte, les lieux de conservation pour les sculptures d'Auguste Rodin qui ont été créées avant le XXème siècle.


#Tableaux de Gustav Klimt
#defaultView:ImageGrid
SELECT ?item ?pic ?location ?coord ?locationLabel ?datecreation
WHERE
{
  ?item wdt:P31 wd:Q860861 . #élément de type sculpture
  ?item wdt:P170 wd:Q30755 . #créateur = Rodin
  ?item wdt:P571 ?datecreation. # date de création, utile pour l'affichage des oeuvres datant d'avant le XXème siècle
  FILTER (?datecreation < "1900-01-01T00:00:00Z"^^xsd:dateTime) . #filtre sur les oeuvres créées avant le XXème siècle
  
 
  OPTIONAL {  ?item wdt:P18 ?pic } . #option sur l'image afin de ne pas invisibiliser les résultats n'ayant pas d'image
  
  ?item wdt:P276 ?location . #trouve le lieu de conservation des sculptures
  ?location wdt:P625 ?coord .#trouve les coordonnées liées aux lieux (permet d'afficher la carte)
  #Filter { ?item wdt:P276 wdt:Q30.} tentative de filtrer sur les Etats-Unis
  
SERVICE wikibase:label { bd:serviceParam wikibase:language "fr,en" } #affiche les labels
}
Vous pouvez désormais voir la carte mettant en évidence toutes les localisations où nous pouvons trouver des oeuvres de Rodin. J'ai tenté de créer le filtre sur les lieux uniquement aux Etats-Unis. Je l'ai laissé en commentaire.
<iframe style="width: 80vw; height: 50vh; border: none;" src="https://query.wikidata.org/embed.html#%23Tableaux%20de%20Gustav%20Klimt%0A%23defaultView%3AImageGrid%0ASELECT%20%3Fitem%20%3Fpic%20%3Flocation%20%3Fcoord%20%3FlocationLabel%20%3Fdatecreation%0AWHERE%0A%7B%0A%20%20%3Fitem%20wdt%3AP31%20wd%3AQ860861%20.%20%23%C3%A9l%C3%A9ment%20de%20type%20sculpture%0A%20%20%3Fitem%20wdt%3AP170%20wd%3AQ30755%20.%20%23cr%C3%A9ateur%20%3D%20Rodin%0A%20%20%3Fitem%20wdt%3AP571%20%3Fdatecreation.%20%23%20date%20de%20cr%C3%A9ation%2C%20utile%20pour%20l%27affichage%20des%20oeuvres%20datant%20d%27avant%20le%20XX%C3%A8me%20si%C3%A8cle%0A%20%20FILTER%20%28%3Fdatecreation%20%3C%20%221900-01-01T00%3A00%3A00Z%22%5E%5Exsd%3AdateTime%29%20.%20%23filtre%20sur%20les%20oeuvres%20cr%C3%A9%C3%A9es%20avant%20le%20XX%C3%A8me%20si%C3%A8cle%0A%20%20%0A%20%0A%20%20OPTIONAL%20%7B%20%20%3Fitem%20wdt%3AP18%20%3Fpic%20%7D%20.%20%23option%20sur%20l%27image%20afin%20de%20ne%20pas%20invisibiliser%20les%20r%C3%A9sultats%20n%27ayant%20pas%20d%27image%0A%20%20%0A%20%20%3Fitem%20wdt%3AP276%20%3Flocation%20.%20%23trouve%20le%20lieu%20de%20conservation%20des%20sculptures%0A%20%20%3Flocation%20wdt%3AP625%20%3Fcoord%20.%23trouve%20les%20coordonn%C3%A9es%20li%C3%A9es%20aux%20lieux%20%28permet%20d%27afficher%20la%20carte%29%0A%20%20%23Filter%20%7B%20%3Fitem%20wdt%3AP276%20wdt%3AQ30.%7D%20tentative%20de%20filtrer%20sur%20les%20Etats-Unis%0A%20%20%0ASERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22fr%2Cen%22%20%7D%20%23affiche%20les%20labels%0A%7D%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>

Quelques bénéfices :
Coût réduit : bien qu’on ne le voit pas au premier abord, le fait de détecter des régressions pendant le développement réduit le temps en aller-retour entre tests fonctionnels et développement.
Sécurité/Qualité : comme dit précédemment les tests réduisent grandement le nombre de régressions et donc assure l’expérience utilisateur.
Documentation : les tests unitaires peuvent aussi servir de documentation technique à du code complexe

.
Karma : moteur permettant d’exécuter les TU et calculer le code-coverage.
Jasmin : framework de tests unitaires.
Jasmine sera notre langage d’assertion. Il permet de décrire les objets à tester, d’exécuter des commandes avant et après chaque test, et d’évaluer le bon fonctionnement de notre code.

describe : permet de définir un groupe de « specs ».
it : permet de définir une « spec » (ou un test).
expect : pour implémenter les assertions.

Jasmine a les principales fonctions et méthodes suivantes :
Describe : description de l’objet à tester
beforeEach / afterEach : exécution de code avant / après chaque test
it : bloc de description de la fonctionnalité à tester
expect : évaluation du cas à tester

Expect comporte des matchers de comparaison avec la variable ou la méthode que l’on souhaite évaluer. Les principaux sont :
toBe : égalité stricte (équivalent au === javascript)
toEqual : égalité non stricte (comparaison entre objets)
toContain : un Array contient un élément donné, ou une string contient une chaîne donnée
toBeDefined : l’objet doit être défini
toBeNull : la valeur doit être nulle
toBeTruthy / toBeFalsy : la valeur est vraie / fausse (truthy / falsy)
toHaveBeenCalled : une méthode doit avoir été appelée
toHaveBeenCalledWith : une méthode doit avoir été appelée avec des paramètres d’une certaine valeur

Jasmine nous offre la possibilité de mocker des objets ou des méthodes avec :
spyOn : mock de la méthode d’un objet
createSpyObj : mock d’un objet dans son intégralité
Ces mocks peuvent retourner une valeur que nous définissons afin de satisfaire les besoins de nos tests.

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

Jasmine est un framework de tests open-source pour JavaScript.
Une suite de tests Jasmine débute avec un appel à describe, une fonction globale de Jasmine qui prend en considération deux paramètres : une chaîne de caractères et une fonction. La chaîne de caractères représente un titre pour la suite, rappelant généralement ce qui va être testé. La fonction, quant à elle, est un bloc de code qui implémente la suite.
Les spécifications, appelées simplement specs, sont définies par l’appel de la fonction globale it de Jasmine, qui elle aussi prend en paramètre une chaîne de caractères et une fonction. La chaîne de caractères définit le test et la fonction est, à proprement parler, le test. Une spec peut contenir une à plusieurs attentes – expectations. En Jasmine, une expectation est une assertion pouvant être vraie ou fausse. Un test qui passe est un test possédant toutes ses expectations à true. Un test qui échoue possède au moins une expectation à false.
describe("My first suite", function() {
var a = true;
it("contains spec with an expectation", function() {
expect(a).toBe(true);
});
});
Les expectations sont construites à partir de la fonction expect qui prend en argument une valeur, appelée la valeur réelle. Le tout est suivi d’une fonction dite matcher qui prend en argument la valeur attendue.
On utilise généralement des objets bouchonnés (mock) comme dépendances. Ce sont des objets factices créés juste pour les besoins du test.
Jasmine nous propose plusieurs méthodes pour déclarer nos tests :
describe() déclare une suite de tests (un groupe de tests) ;
it() déclare un test ;
expect() déclare une assertion.

NOTE
Une astuce : si tu utilises fdescribe() au lieu de describe() alors cette seule
suite de tests sera exécutée (le "f" ajouté signifie "focus").
Même chose si tu ne veux exécuter qu’un seul test : utilise fit()au lieu de it().
Si tu veux exclure un test, utilise xit(), ou xdescribe() pour une suite de tests.

BEFORE ET AFTER
Il est possible d’exécuter du code avant ou après chacune des specs écrites, respectivement grâce aux fonctionnalités beforeEach et afterEach. Cela peut devenir très pratique si l’on veut factoriser du code, ou si l’on utilise des variables globales que l’on soit réinitialisé après un test.
describe("My first suite with 'beforeEach' and 'afterEach'", function() {
var a = 0;

beforeEach(function() {
a += 1;
});

afterEach(function() {
a = 0;
});

it("checks the value of a", function() {
expect(a).toEqual(1);
a += 1;
});

it("expects a to still be equal to 1", function() {
expect(a).toEqual(1);
});
});
Il est également possible d’exécuter du code avant ou après toutes les specs contenues dans une suite. Comme le suggère son nom, la fonction beforeAll est appelée avant l’exécution de toutes les specs, et afterAll est appelée après l’exécution de toutes les specs.
LES MATCHERS
Un matcher produit une comparaison booléenne entre la valeur réelle d’un élément et sa valeur attendue. Si ces deux valeurs sont divergentes, l’expectation est considérée comme fausse, et Jasmine fait échouer la spec.
Un matcher peut aussi être évalué avec une assertion négative. Il suffit pour cela d’ajouter le mot clé not avant l’utilisation du matcher.
describe("My first suite", function() {
var a = true;

it("contains spec with an expectation", function() {
expect(a).not.toBe(false);
});
});
TOBE
Le matcher toBe compare deux valeurs entre elles grâce à l’opérateur === en JavaScript.
describe("The 'toBe' matcher", function() {
var a = 1,
b = 2;

it("compares with ===", function() {
expect(a + b).toBe(3);
expect(a).not.toBe(b);
});
});
TOEQUAL
Le matcher toEqual permet de vérifier l’équivalence de deux valeurs. toBe est donc plus strict que toEqual.
describe("The 'toEqual' matcher", function() {
it("works with simple variables", function() {
var a = 4;
expect(a).toEqual(4);
});

it("works also well with arrays", function() {
var b = new Array('1', '2'),
c = new Array('1', '2');
expect(b).toEqual(c);
});
});
TOMATCH
Le matcher toMatch permet la comparaison avec les expressions régulières. Il permet de tester la bonne structure d’une valeur selon un pattern bien défini.
toMatch fonctionne également avec les chaînes de caractères, qui seront ensuite analysées comme des expressions régulières.
describe("The 'toMatch' matcher", function() {
var message = "hello world!";

it("compares with RegExp", function() {
expect(message).toMatch(/^hello/);
expect(message).toMatch("hello");
expect(message).toMatch(/world!$/);
expect(message).not.toMatch(/boy/);
});
});
TOBENULL
toBeNull permet de tester la nullité d’un élément. Si cet élément possède une valeur dite null, alors l’expectation sera considérée true. Le cas échéant, Jasmine fait échouer la spec.
describe("The 'toBeNull' matcher", function() {
var a = null,
b = "test";

it("compares with null", function() {
expect(a).toBeNull();
expect(b).not.toBeNull();
});
});
TOCONTAIN
toContain permet de vérifier la présence d’un élément dans un tableau.
describe("The 'toContain' matcher", function() {
var a = ["banana", "pineapple", "coconut"];

it("finds an item in an Array", function() {
expect(a).toContain("banana");
expect(a).not.toContain("strawberry");
});
});
toContain fonctionne également avec les chaînes de caractères : la fonction permet alors de vérifier si un ensemble de caractères figurent dans la chaîne globale.
describe("The 'toContain' matcher", function() {
var a = "The quick brown fox jumps over the lazy dog";

it("finds a substring in an String", function() {
expect(a).toContain("fox");
expect(a).not.toContain("foxy");
});
});
TOBETRUTHY ET TOBEFALSY
Les matchers toBeTruthy et toBeFalsy permettent de tester de manière booléenne des valeurs. En JavaScript, tous types de valeurs peuvent être utilisés pour obtenir une valeur booléenne, par exemple lors de l’utilisation de la déclaration conditionnelle if.
Les valeurs suivantes seront interprétées comme étant false : undefined, null, false, 0, NaN et la chaîne de caractères vide "". Toutes les autres valeurs – objets et tableaux compris – sont considérées comme true. Les valeurs interprétées comme false sont appelées falsy, et les valeurs interprétées comme true sont appelées truthy.
Boolean(), appelé en tant que fonction, convertit son paramètre en booléen. Vous pouvez utiliser cette fonction pour savoir comment une valeur sera interprétée.
describe("The 'toBeTruthy' and 'toBeFalsy' matchers", function() {
var a,
b = false,
c = 15;

it("is for boolean casting testing", function() {
expect(a).toBeFalsy();
expect(a).not.toBeTruthy();
});

it("is for boolean casting testing", function() {
expect(b).toBeFalsy();
expect(b).not.toBeTruthy();
});

it("is for boolean casting testing", function() {
expect(c).toBeTruthy();
expect(c).not.toBeFalsy();
});
});
TOBEDEFINED ET TOBEUNDEFINED
toBeDefined et toBeUndefined permettent de vérifier l’existence ou non d’une valeur. À noter une nouvelle fois que la valeur de type undefined est aussi considérée comme étant false.
En JavaScript, les variables non-initialisées ne possèdent pas de valeur, elles sont undefined. Une propriété inexistante pour un objet renvoie également une valeur dite undefined. Une fonction qui ne possède pas de return, ou une fonction possédant un return vide, est une fonction qui retourne undefined.
describe("The 'toBeDefined' and 'toBeUndefined' matchers", function() {
var a,
b = 3,
c = (function() {})();

it("compares against `defined`", function() {
expect(a).not.toBeDefined();
expect(b).toBeDefined();
expect(c).not.toBeDefined();
});

it("compares against `undefined`", function() {
expect(a).toBeUndefined();
expect(b).not.toBeUndefined();
expect(c).toBeUndefined();
});
});
TOBELESSTHAN ET TOBEGREATERTHAN
toBeGreaterThan et toBeLessThan permettent de vérifier si un élément est plus grand, ou s’il est plus petit, qu’un autre.
describe("The 'toBeLessThan' and 'toBeGreaterThan' matchers", function() {
var a = 1,
b = 2,
c = 3;

it("is for mathematical comparisons", function() {
expect(a).toBeLessThan(b);
expect(b).not.toBeGreaterThan(c);
expect(c).not.toBeLessThan(a);
});
});

Appréhender la syntaxe de Jasmine
Une suite de tests Jasmine débute avec un appel à describe, une fonction globale de Jasmine qui prend en considération deux paramètres : une chaîne de caractères et une fonction. La chaîne de caractères représente un titre pour la suite, rappelant généralement ce qui va être testé. La fonction, quant à elle, est un bloc de code qui implémente la suite.
Les « spécifications », appelées simplement specs, sont définies par l’appel de la fonction globale it de Jasmine, qui elle aussi prend en paramètre une chaîne de caractères et une fonction. La chaîne de caractères définit le test et la fonction est, à proprement parler, le test. Une spec peut contenir une à plusieurs « attentes » – expectations. En Jasmine, une expectation est une assertion pouvant être vraie ou fausse. Un test qui passe est un test possédant toutes ses expectations à true. Un test qui échoue possède au moins une expectation à false.
describe("My first suite", function() {
it("contains spec with an expectation", function() {
expect(true).toBe(true);
});
});

Les blocs describe et it sont des fonctions. Celles-ci peuvent donc contenir tout le code nécessaire à l’exécution des tests. Les règles classiques de scope en JavaScript s’y appliquent ; ce qui signifie que toutes les variables déclarées dans un bloc describe seront disponibles dans chacun des blocs it que possède la suite.
describe("My first suite", function() {
var a = true;

it("contains spec with an expectation", function() {
expect(a).toBe(true);
});
});

Les expectations sont construites à partir de la fonction expect qui prend en argument une valeur, appelée la valeur réelle. Le tout est suivi d’une fonction dite matcher qui prend en argument la valeur attendue.
before et after
Il est possible d’exécuter du code « avant » ou « après » chacune des specs écrites, respectivement grâce aux fonctionnalités beforeEach et afterEach. Cela peut devenir très pratique si l’on veut factoriser du code, ou si l’on utilise des variables globales que l’on souhaite réinitialiser après un test.
describe("My first suite with 'beforeEach' and 'afterEach'", function() {
var a = 0;

beforeEach(function() {
a += 1;
});

afterEach(function() {
a = 0;
});

it("checks the value of a", function() {
expect(a).toEqual(1);
a += 1;
});

it("expects a to still be equal to 1", function() {
expect(a).toEqual(1);
});
});

Il est également possible d’exécuter du code « avant » ou « après » toutes les specs contenues dans une suite. Comme le suggère son nom, la fonction beforeAll est appelée avant l’exécution de toutes les specs, et afterAll est appelée après l’exécution de toutes les specs.
describe("My first suite with 'beforeAll' and 'afterAll'", function() {
var a;

beforeAll(function() {
a += 1;
});

afterAll(function() {
a = 0;
});

it("checks the value of a", function() {
expect(a).toEqual(1);
a += 1;
});

it("does not reset a between specs", function() {
expect(a).toEqual(2);
});
});

Les matchers
Un matcher produit une comparaison booléenne entre la valeur réelle d’un élément et sa valeur attendue. Si ces deux valeurs sont divergentes, l’expectation est considérée comme fausse, et Jasmine fait échouer la spec.
Un matcher peut aussi être évalué avec une assertion négative. Il suffit pour cela d’ajouter le mot-clé not avant l’utilisation du matcher.
describe("My first suite", function() {
var a = true;

it("contains spec with an expectation", function() {
expect(a).not.toBe(false);
});
});

Un grand nombre de matchers sont disponibles nativement dans Jasmine.
TOBE
Le matcher toBe compare deux valeurs entre elles grâce à l’opérateur === en JavaScript.
describe("The 'toBe' matcher", function() {
var a = 1,
b = 2;

it("compares with ===", function() {
expect(a + b).toBe(3);
expect(a).not.toBe(b);
});
});

TOEQUAL
Le matcher toEqual permet de vérifier l’équivalence de deux valeurs. toBe est donc plus strict que toEqual.
describe("The 'toEqual' matcher", function() {
it("works with simple variables", function() {
var a = 4;
expect(a).toEqual(4);
});

it("works also well with arrays", function() {
var b = new Array('1', '2'),
c = new Array('1', '2');
expect(b).toEqual(c);
});
});

TOMATCH
Le matcher toMatch permet la comparaison avec les expressions régulières. Il permet de tester la bonne structure d’une valeur selon un pattern bien défini.
toMatch fonctionne également avec les chaînes de caractères, qui seront ensuite analysées comme des expressions régulières.
describe("The 'toMatch' matcher", function() {
var message = "hello world!";

it("compares with RegExp", function() {
expect(message).toMatch(/^hello/);
expect(message).toMatch("hello");
expect(message).toMatch(/world!$/);
expect(message).not.toMatch(/boy/);
});
});

TOBENULL
toBeNull permet de tester la nullité d’un élément. Si cet élément possède une valeur dite null, alors l’expectation sera considérée true. Le cas échéant, Jasmine fait échouer la spec.
describe("The 'toBeNull' matcher", function() {
var a = null,
b = "test";

it("compares with null", function() {
expect(a).toBeNull();
expect(b).not.toBeNull();
});
});

TOCONTAIN
toContain permet de vérifier la présence d’un élément dans un tableau.
describe("The 'toContain' matcher", function() {
var a = ["banana", "pineapple", "coconut"];

it("finds an item in an Array", function() {
expect(a).toContain("banana");
expect(a).not.toContain("strawberry");
});
});

toContain fonctionne également avec les chaînes de caractères : la fonction permet alors de vérifier si un ensemble de caractères figurent dans la chaîne globale.
describe("The 'toContain' matcher", function() {
var a = "The quick brown fox jumps over the lazy dog";

it("finds a substring in an String", function() {
expect(a).toContain("fox");
expect(a).not.toContain("foxy");
});
});

TOBETRUTHY ET TOBEFALSY
Les matchers toBeTruthy et toBeFalsy permettent de tester de manière booléenne des valeurs. En JavaScript, tous types de valeurs peuvent être utilisés pour obtenir une valeur booléenne, par exemple lors de l’utilisation de la déclaration conditionnelle if.
Les valeurs suivantes seront interprétées comme étant false : undefined, null, false, 0, NaN et la chaîne de caractères vide "". Toutes les autres valeurs – objets et tableaux compris – sont considérées comme true. Les valeurs interprétées comme false sont appelées falsy, et les valeurs interprétées comme true sont appelées truthy.
Boolean(), appelé en tant que fonction, convertit son paramètre en booléen. Vous pouvez utiliser cette fonction pour savoir comment une valeur sera interprétée.
describe("The 'toBeTruthy' and 'toBeFalsy' matchers", function() {
var a,
b = false,
c = 15;

it("is for boolean casting testing", function() {
expect(a).toBeFalsy();
expect(a).not.toBeTruthy();
});

it("is for boolean casting testing", function() {
expect(b).toBeFalsy();
expect(b).not.toBeTruthy();
});

it("is for boolean casting testing", function() {
expect(c).toBeTruthy();
expect(c).not.toBeFalsy();
});
});

TOBEDEFINED ET TOBEUNDEFINED
toBeDefined et toBeUndefined permettent de vérifier l’existence ou non d’une valeur. À noter une nouvelle fois que la valeur de type undefined est aussi considérée comme étant false.
En JavaScript, les variables non initialisées ne possèdent pas de valeur, elles sont undefined. Une propriété inexistante pour un objet renvoie également une valeur dite undefined. Une fonction qui ne possède pas de return, ou une fonction possédant un return vide, est une fonction qui retourne undefined.
describe("The 'toBeDefined' and 'toBeUndefined' matchers", function() {
var a,
b = 3,
c = (function() {})();

it("compares against `defined`", function() {
expect(a).not.toBeDefined();
expect(b).toBeDefined();
expect(c).not.toBeDefined();
});

it("compares against `undefined`", function() {
expect(a).toBeUndefined();
expect(b).not.toBeUndefined();
expect(c).toBeUndefined();
});
});

TOBELESSTHAN ET TOBEGREATERTHAN
toBeGreaterThan et toBeLessThan permettent de vérifier si un élément est plus grand, ou s’il est plus petit, qu’un autre.
describe("The 'toBeLessThan' and 'toBeGreaterThan' matchers", function() {
var a = 1,
b = 2,
c = 3;

it("is for mathematical comparisons", function() {
expect(a).toBeLessThan(b);
expect(b).not.toBeGreaterThan(c);
expect(c).not.toBeLessThan(a);
});
});

TOBECLOSETO
toBeCloseTo permet de vérifier si un nombre est proche d’un nombre, selon un certain nombre de décimales, donné en deuxième argument du matcher.
describe("The 'toBeCloseTo' matcher", function() {
var a = 1.2,
b = 1.25;

it("is for precision math comparison", function() {
expect(b).toBeCloseTo(a, 1);
expect(b).not.toBeCloseTo(a, 2);
});
});

En utilisant deux décimales dans l’exemple ci-dessous, toBeCloseTo considère que le deuxième chiffre décimal diffère pour les deux nombres choisis. Mettre le deuxième argument à 0 arrondit les nombres aux entiers.
toBeCloseTo est assez difficile à prendre en main. Je vous recommande de bien tester son comportement avant de le mettre en œuvre dans plusieurs de vos tests.
TOTHROW ET TOTHROWERROR
toThrow permet de tester les erreurs. En utilisant ce matcher, Jasmine s’attend à recevoir une erreur, et c’est donc seulement en présence de celle-ci que la spec passera.
toThrowError permet de tester spécifiquement des erreurs. Ce matcher autorise en argument une expression régulière, une chaîne de caractères ou un type d’erreur.
describe("The 'toThrow' matcher", function() {
var f = function(){ throw new Error(); },
g = function(){ throw new TypeError("I failed!"); };

it("tests if a function throws an exception", function() {
expect(f).toThrow();
});

it("tests a specific thrown exception", function() {
expect(g).toThrowError(/fail/);
expect(g).toThrowError("I");
expect(g).toThrowError(TypeError);
});
});

DES MATCHERS PERSONNALISÉS
Il est également possible de créer ses propres matchers. Il faut ajouter son matcher au sein du fichier contenant les specs qui doivent l’utiliser. Pour cela, il est possible d’utiliser beforeEach ou beforeAll.
Dans les versions de Jasmine supérieures à la 2.0, la fonction compare reçoit la valeur passée à la fonction expect comme étant son premier argument, la valeur réelle, et la valeur (si celle-ci existe) donnée au matcher comme étant son deuxième argument, la valeur attendue. Les matchers personnalisés prennent en argument deux paramètres : util, qui est un set de fonctions utiles pour les matchers, voir matchersUtil.js pour une liste détaillée ; et customEqualityTesters, qui a besoin d’être appelé si util.equals est utilisé.
Dans le cas présent ci-dessous, un matcher est créé ne prenant en considération que la valeur réelle, actual, et je vérifie si celle-ci est paire grâce à util.equals. Cette fonction prend en paramètre la valeur réelle, la valeur attendue, et l’objet customEqualityTesters. La valeur réelle est ici, une opération avec modulo 2 qui consiste à vérifier si mon nombre est pair, et la valeur attendue est true. Si jamais cette opération donne un résultat égal à false, le matcher toBeEven me renvoie le message « Expected <number> to be even » et la spec échoue.
describe("The 'toBeEven' matcher", function() {
beforeAll(function() {
jasmine.addMatchers({
toBeEven: function(util, customEqualityTesters) {
return {
compare: function(actual){
return { pass: util.equals(actual%2==0, true, customEqualityTesters) }
}
}
this.message = function() {
return "Expected " + actual + " to be even";
};
}
});
});

if('expects numbers to be even or not', function(){
expect(2).toBeEven();
expect(6857).not.toBeEven();
});
});

Un peu de pratique est nécessaire pour bien comprendre comment mettre en place ses propres matchers. Mais vous verrez que les possibilités sont énormes, et que cela peut vous permettre d’avoir un code plus lisible si vos suites possèdent beaucoup de specs.
Écrire un premier test Jasmine
Ainsi, il est, par exemple, très simple de vérifier à l’aide de Jasmine, le bon comportement de la fonction du crible d’Eratosthenes présente ci-dessous. Cette fonction est censée retourner un tableau de tous les nombres premiers inférieurs à n.
function eratosthenes(n) {
var detectprimes = new Array(n),
primes = new Array();

detectprimes[0] = false;
detectprimes[1] = false;

for(var i=2; i < detectprimes.length; i++)
detectprimes[i] = true;

for(var p=2; p < Math.sqrt(n); p++) {
if(detectprimes[p]) {
for(var j = p\*p; j < n; j+= p)
detectprimes[j] = false;
}
}

for (var i = 0; i < n; i++)
if(detectprimes[i]) primes.push(i);

return primes;
}

Dans la suite créée, on souhaite obtenir un tableau de tous les nombres premiers en-dessous de 100. Pour cela, on utilise la fonction eratosthenes avec en paramètre le nombre 100.
Le test doit effectuer les vérifications suivantes. Ce tableau doit contenir 25 éléments. Parmi eux doivent figurer les nombres 5, 11, 43 et 97, choisis de façon totalement arbitraire. Mais les nombres 28, 60 et 99 ne doivent pas appartenir à ce tableau, car ils ne sont pas premiers.
describe('Prime numbers under 100 array', function(){
var primes = eratosthenes(100);

it('is truthy', function(){
expect(primes).toBeTruthy();
});

it('is really an array', function(){
expect(Array.isArray(primes)).toBe(true);
});

it('has 25 primes under 100', function(){
expect(primes.length).toEqual(25);
});

it('contains 5, 11, 43, 97 as primes', function(){
expect(primes).toContain(5);
expect(primes).toContain(11);
expect(primes).toContain(43);
expect(primes).toContain(97);
});

it('does not contain 28, 60, 99', function(){
expect(primes).not.toContain(28);
expect(primes).not.toContain(60);
expect(primes).not.toContain(99);
});
});

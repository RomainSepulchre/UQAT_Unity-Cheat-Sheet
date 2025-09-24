# Unity cheat sheet

## Variables

Une variable est un emplacement de mémoire qui contient une donnée que l'on garde pour la réutiliser à différents endroits du code.

(Exemple) Comment une variable est déclaré.
```c#
// Niveau accessiblitié | Type de la variable | Nom de la variable | valeur assigné
    public                  int                     MyInt               = 1;
```

### Type d'une variable

Une variable est définit par un type qui spécifie le type de donnée que la variable va contenir. Le type peut être un type de base comme un entier(``int``) ou une chaine de caractère(``string``) mais ça peut aussi être une classe que vous avez créer.

### Accessibilité de la variable

Lorsque l'on déclare une variable, on définit généralement aussi son niveau d'accessibilité. Les deux niveaux les plus utilisés sont ``public`` et ``private``.

- ``public``: la variable est accessible depuis n'importe quel autre classe. Dans unity, elle est aussi accesible dans l'inspecteur par défaut.
- ``private``: la variable est accessible uniquement à l'intérieur de la classe. Dans unity, elle ne sera pas accessible dans l'inspecteur par défaut.

> Une variable dont on ne définit pas l'accessibilité est ``private`` par défaut.

### Assigner une valeur

Lorsque l'on déclare une variable on peut directement lui assigner une valeur par défaut mais ce n'est pas obligatoire.

### Exemple de déclaration de variables

```c#
public int MyInt = 0; // privé
private float = 1f; // public
string MyString = "some text"; // variable privée car l'accessibilité n'est pas définit
public MyClass SomeData; //  Type = MyClass (classe créer par l'utilisateur)
```
## Class

### C'est quoi une classe ?

Une classe est une structure de données. Elle définit un objet qui est caractérisé par des **variables**, un **constructeur** et des **méthodes**.

- **Variables**: Informations contenus dans la classe.
- **Constructeur**: Définit comment créer un objet du type de la classe mais n'est pas obligatoire.
- **Méthodes**: Une méthode définit une suite d'opérations à faire avec les données de la classe.

(Exemple) Créer une classe qui représente une personne:
```c#
// Exemple d'un classe qui représente une personne
public class Person
{
    // Variables de la classe
    public string FirstName;
    public string LastName;

    // Constructeur (Pas obligatoire mais définit comment créer un objet de type MyClass)
    public Person (string _firstName, string _lastName)
    {
        FirstName = _firstName;
        LastName = _lastName;
    }

    // Méthodes de la classe
    public void LogName()
    {
        Debug.Log($"{FirstName} {LastName}")
    }
}
```

(Exemple) Création d'un objet de type *Person*: 
```c#
// Exemple de comment créer un objet de type Person
Person someone = new Person("Romain", "Sepulchre");

// Afficher les infos de l'objet dans la console avec la méthode LogName()
someone.LogName(); // => Romain Sepulchre
```

### Imbriquer des classes

Une classe contenir une autre classe. La classe contenu est alors accessible uniquement à partir de la classe qui la contient.

(Exemple) Ajout d'une classe pour la date de naissance dans la classe *Person*: 
```c#
public class Person
{
    // Classe BirthDate définit à l'intérieur de Person
    public class BirthDate
    {
        public int Day;
        public int Month;
        public int Year;

        public BirthDate (int _day, int _month, int _year)
        {
            Day = _day;
            Month = _month;
            Year = _year;
        }
    }

    // Variables de la classe
    public string FirstName;
    public string LastName;
    public BirthDate DateOfBirth; // On peut créer une variable avec notre classe BirthDate à l'intérieur de la classe Person

    // Constructeur
    public Person (string _firstName, string _lastName, BirthDate _dateOfBirth)
    {
        FirstName = _firstName;
        LastName = _lastName;
        DateOfBirth = _dateOfBirth;
    }
}
```

(Exemple) Créer un objet de type *Person* avec la classe *BirthDate*
```c#
Person.BirthDate dateOfBirth = new Person.BirthDate(18, 06, 1994);
Person someone = new Person("Romain", "Sepulchre", dateOfBirth);
```

### Hériter d'une classe

Il est possible d'hériter des caractéristiques d'une classe, la classe enfant récupère toutes les caractéristiques et les méthodes publiques de la classe parent. La classe enfant peut ainsi avoir des caractéristiques propre tout en conservant les caractéristiques définit dans la classe dont elle hérite.

(Exemple) Avec la classe *Person* on pourrait créer une classe *Adult* et une classe *Children* qui éeritent toutes les deux de *Person*:

```c#
public class Adult : Person // Adult hérite de Person
{
    // Adult peut avoir des variables spécifiques par exemple un travail
    public string Work;

    // Constructeur de la classe Adult
    public Adult(string _firstName, string _lastName, BirthDate _dateOfBirth, string _work) : base(_firstName, _lastName, _dateOfBirth)
    {
        FirstName = _firstName;
        LastName = _lastName;
        DateOfBirth = _dateOfBirth;
        Work = _work;
    }
}

public class Children : Person // Children hérite de Person
{
    // Children peut avoir des variables spécifiques par exemple une école
    public string School;

    // Constructeur de la classe Children
    public Children(string _firstName, string _lastName, BirthDate _dateOfBirth, string _school) : base(_firstName, _lastName, _dateOfBirth)
    {
        FirstName = _firstName;
        LastName = _lastName;
        DateOfBirth = _dateOfBirth;
        School = _school;
    }
}
```

## Types de variables

### Int

Nombre entier:
```C#
public int MyInt = 1;
```

### Float

Nombre avec virgule:
```C#
public float MyFloat = 1.0f; // un float est toujours défini avec un f après la valeur
```

### Bool

Variable qui peut seulement avoir 2 états: vrai ou faux.

```C#
public bool MyBool = true; // un bool peut seulement être true ou false
```

### String

Texte (Chaine de caractères):
```C#
public string MyString = "some text"; // un string est toujours défini entre guillemets ("")
```

### Vector 3

Vecteur 3D (x,y,z):
```C#
public Vector3 MyVector3 = new Vector3(1.0f, 0.5f, 3);
MyVector3.x // = 1.0f
MyVector3.y // = 0.5f
MyVector3.z // = 3
```

### Vector2

Vecteur 2D (x,y):
```C#
public Vector2 MyVector2 = new Vector2(2.5f, 0.3f);
MyVector3.x // = 2.5f
MyVector3.y // = 0.3f
```

### Quaternion
Les Quaternions sont une manière abstraite de calculer la rotation d'un objet.

Pour des raisons de performances et pour éviter les problèmes de *gimbal lock*, les valeurs de rotations sont calculé avec des Quaternions mais affiché en degré (angles d'euler = rotation x, rotation y, rotation z).

```C#
// Créer un Quaternion en donnant des valeurs d'angles en degrées
public Quaternion NewRotation = Quaternion.Euler(90f,0 ,0); // Tourné à 90 degrée sur l'angle x
```

## Structures de données (Tableaux, Listes, ...)

### Array (Tableau)

Il est possible de créer des tableaux d'une taille défini pour stocker des données.

Tableau avec une ligne:  
| 1    | 2    | 3    |

```c#
// Tableau de int avec 3 colonnes
public int[] IntArrayA = new int[3];
IntArrayA[0] = 1;
IntArrayA[2] = 2;
IntArrayA[3] = 3;

// Tableau de int avec 5 colonnes (les valeurs sont défini durant la déclaration)
public int[] IntArrayB = [5, 10, 15, 20, 25]
IntArrayB[4]; // Colonne 4 = 20
```

#### Array2D (Tableau 2D)

Tableau avec plusieurs lignes et plusieurs colonnes:

| 1    | 2    | 3    |  
| 4    | 5    | 6    |  
| 7    | 8    | 9    |  

```c#
// Tableau de int avec 3 lignes et 3 colonnes
public int[,] Int2dArrayA = new int[3,3]
// Remplir première ligne
Int2dArrayA[0,0] = 1;
Int2dArrayA[0,1] = 2;
Int2dArrayA[0,2] = 3;
// Remplir seconde ligne
Int2dArrayA[1,0] = 4;
Int2dArrayA[1,1] = 5;
Int2dArrayA[1,2] = 6;

// Tableau de int avec 3 lignes et 3 colonnes (les valeurs sont défini durant la déclaration)
public int[,] Int2dArrayB = new int[,,] { {1,2,3}, {4,5,6}, {7,8,9} }
IntArrayB[1,2]; //  2ème ligne, 3ème colonne = 6
```

> Les tableaux ne sont pas limités à 2D, ils peuvent aussi être 3D ``int[,,]`` par exemple.

### List

Les tableaux sont pratiques mais ils nécessitent de d'avoir une taille défini. Pour avoir plus de flexibilité on peut utiliser une liste. La taille de la liste se met à jour automatiquement lorsque l'on enlève on rajoute une entrée dans la liste.

```c#
public List<string> MyStringList = new List<string>();

// Ajouter éléments
MyStringList.Add("First entry");
MyStringList.Add("Second entry");
MyStringList.Add("Third entry");

// Enlever éléments 
MyStringList.Remove("Third entry"); // Enlève cette de chaîne caractère de la liste (si elle existe)
MyStringList.RemoveAt(2); // Enlève élement à un index précis (si l'index existe)
```

### Dictionnary

Les dictionnaires permettent de stocker des données par paire. La paire de donnée est composé d'une clé, et d'une valeur.

La clé est utilisé pour accéder à la valeur. Si on fait le parrallèle avec un tableau, pour accéder à une variable on fournit un index pour préciser a quel case on veut accéder (ex: ``Array[1]``, ici 1 est l'index auquel on veut accéder). Avec un dictionnaire plutôt que d'utiliser un index on utilise une autre variable pour accéder à la valeur. La puissance du dictionnaire repose sur le fait que la clé n'a pas nécessairement besoin d'être un nombre entier, n'importe quel type de variable peut être utilisé comme une clé  

```c#
// On déclare un dictionnaire ou la clé est une string et la valeur est un int
Dictionnary<string, int> NumberDictionnary = new Dictionnary<string, int>();

// Ajouter éléments dans le dictionnaire
NumberDictionnary.Add("zero", 0); // pour accéder au int 0 on utilise la clé "zero"
NumberDictionnary.Add("dix", 10); // pour accéder au int 10 on utilise la clé "dix"
NumberDictionnary.Add("vingt", 20); // pour accéder au int 20 on utilise la clé "vingt"

// Accéder à une valeur dans le dictionnaire
NumberDictionnary["zero"]; // = 0
NumberDictionnary["dix"]; // = 10
NumberDictionnary["vingt"]; // = 20

// La clé et la valeur peuvent être n'importe quel type de variable, voici un autre exemple de dictionnaire:
Dictionnary<Vector3, Vector3> DirectionDictionnary = new Dictionnary<string, Vector3>(); // clé = Vector3 , valeur = string

DirectionDictionnary.Add(new Vector3(1,0,0), "left"); // pour accéder à "left" on utilise un vector3 comme clé (1,0,0)
DirectionDictionnary.Add(new Vector3(0,1,0), "up"); // pour accéder à "up" on utilise un vector3 comme clé (0,1,0)
DirectionDictionnary.Add(new Vector3(0,0,1), "forward"); // pour accéder à "forward" on utilise un vector3 comme clé (0,0,1)

DirectionDictionnary[new Vector3(1,0,0)]; // = "left"
DirectionDictionnary[new Vector3(0,1,0)]; // = "up"
DirectionDictionnary[new Vector3(0,0,1)]; // = "forward"
```

## Fonctions

Une fonction est un ensemble d'instructions réutilisables. Par exemple, si je sais que je dois activer plusieurs objets à différents endroits de mon code plutôt que de reécrire les même lignes plusieurs fois je peux faire une fonction et appeler directement cette fonction.

### Déclarer une fonction

```c#
// Niveau accessiblitié | Type de la variable retourné | Nom de la fonctions | Paramètres
    public                      void                        MyInt               (int someInt)
    {
        // Instructions appelées par la fonction
    }
```

- *Accessibilité*: comme les variables, les fonctions peuvent être ``public`` ou ``private`` pour définir si la fonction sera accessible en dehors de la classe ou non.
- *Type retourné*: une fois qu'une fonction a terminé ses instructions elle peut renvoyer une valeur. Le type de la valeur a retourner est défini ici. Si la fonction en renvoie aucune donnée on utilise le type ``void`` pour préciser qu'on en retourne pas de données.
- *Paramètres*: Si nécessaire, on peut fournir des paramètres à utiliser dans les instructions exécuté. Par exemple, en ajoutant un paramètre ``bool`` à une fonction qui active des objets on peut définir si la fonction doit activer ou désactiver les objets au moment de l'appel de la fonction plutôt que dans les instructions de la fonction.

### Fonction simple 

```c#
// Exemple d'une fonction qui active des objets
public void ActivateObjects()
{
    ObjectA.SetActive(true);
    ObjectB.SetActive(true);
    ObjectC.SetActive(true);
}

// Appeler la fonction ActivateObjects()
ActivateObjects();
```

### Fonction avec paramètre

```c#
// Exemple d'une fonction qui active ou désactive des objets en fonction du paramètre enable reçu par la fonction
public void ActivateObjects(bool enable)
{
    ObjectA.SetActive(enable);
    ObjectB.SetActive(enable);
    ObjectC.SetActive(enable);
}

// Appeler la fonction ActivateObjects()
ActivateObjects(true); // Activer objets
ActivateObjects(false); // Désactiver objets
```

### Fonction qui retourne une valeur

```c#
// Exemple d'une fonction qui additionne deux nombres entiers et retourne le résultat
public int Addition(int firstNumber, int secondNumber) // le type de retour a été défini comme int plutôt que void
{
    int result = firstNumber + secondNumber; // Calculer le résultat de l'addition
    return result; // on appelle return suivi de la variable à renvoyer pour terminer la fonction et renvoyer la valeur de la variable result  
}

// Appeler la fonction Addition()
int additionResult = Addition(1, 1); // On créer une variable int pour récupérer le résultat de la fonction Addition().
additionResult; // = 2 (1 + 1)
```

## Evènements Unity

Voir https://moodle.uqat.ca/pluginfile.php/1686134/mod_resource/content/1/Guide-to-the-Execution-Order-of-Unity-Event-Functions-V2-Light.png 

### Awake

Appelé une fois lorsque que l'objet devient actif pour la toute première fois.

```c#
void Awake()
{
}
```

### OnEnable

Appelé à chaque fois que l'objet est activé.

```c#
void OnEnable()
{
}
```

### Start

Appelé une seule fois lorque que le component devient actif pour la première fois. Toujours appelé avant la première Update.

```c#
void Start()
{
}
```

### Update

Appelé à chaque frame.

```c#
void Update()
{
}
```

### OnDisable

Appelé à chaque fois que l'objet est désactivé.

```c#
void OnDisable()
{
}
```

### OnDestroy

Appelé lorsque l'objet va être détruit.

```c#
void OnDestroy()
{
}
```

### Évènements physiques (collisions et trigegr)

#### OnCollisionEnter

Appelé à chaque fois que l'objet entre en collision avec un autre objet.

L'évènement envoie aussi des informations sur l'objet avec lequel la collision vient d'arriver dans ``Collision other``.

```c#
void OnCollisionEnter(Collision other)
{
}
```

#### OnCollisionStay

Appelé tant que l'objet reste en collision avec un autre objet.

L'évènement envoie aussi des informations sur l'objet avec lequel la collision continue de se produire dans ``Collision other``.

```c#
void OnCollisionStay(Collision other)
{
}
```

#### OnCollisionExit

Appelé lorsque l'objet n'est plus en collision avec un objet avec lequel il était en collision auparavant.

L'évènement envoie aussi des informations sur l'objet avec lequel la collision vient de s'arrêter dans ``Collision other``.

```c#
void OnCollisionExit(Collision other)
{
}
```

### Évènements de trigger

#### OnTriggerEnter

Appelé à chaque fois que l'objet entre dans un trigger.

L'évènement envoie aussi des informations sur le trigger dans lequel l'objet vient d'entrer dans ``Collider other``.

```c#
void OnTriggerEnter(Collider other)
{
}
```

#### OnTriggerStay

Appelé tanat que l'objet reste dans un trigger.

L'évènement envoie aussi des informations sur le trigger dans lequel l'objet reste dans ``Collider other``.

```c#
void OnTriggerStay(Collider other)
{
}
```

#### OnTriggerExit

Appelé lorsque l'objet sort d'un trigger dans lequel il était auparavant.

L'évènement envoie aussi des informations sur le trigger que l'objet vient de quitter dans ``Collider other``.

```c#
void OnTriggerExit(Collider other)
{
}
```

## GameObject et component

Chaque classe qui hérite de Monobehaviour peut automatiquement accéder à l'objet sur lequel le script est placé et au transform de cet objet.
- ``gameObject``: permet d'accéder au gameObject sur lequel le script est placé.
- ``transform``: permet d'accéder au transform sur lequel le script est placé.

### Accéder à un component



#### GetComponent

```c#
// Définir une variable pour récupérer le component avec la fonction GetComponent()
BoxCollider collider = GetComponent<BoxCollider>()

// Faire quelque chose avec le BoxCollider trouvé
collider.isTrigger = true; // (ex: Activer isTrigger sur le BoxCollider)
```

#### TryGetComponent

```c#
// Variante de GetComponent qui vérifie si le component existe (plus performante car n'alloue pas de mémoire si le component n'existe pas)
BoxCollider collider;
bool componentFound = TryGetComponent<BoxCollider>(out collider);

if(componentFound)
{
    // Faire quelque chose avec le BoxCollider trouvé
    collider.isTrigger = true; // (ex: Activer isTrigger sur le BoxCollider)
}
```

#### Reférence directe

```c#
// Déclarer une variable public pour le component pour le linker dans la fenêtre d'inspecteur
public BoxCollider collider;
```

### Créer un GameObject

```c#
GameObject objectToSpawn;
Instantiate(objectToSpawn);
```

### Détruire un GameObject

```c#
GameObject objectToDestroy;
Destroy(objectToDestroy);
```

### Trouver un GameObject dans une scène

#### Find

```c#
// Chercher un objet à partir de son nom
GameObject.Find("ObjectName"); // ObjectName est le nom de l'objet que vous recherchez
```

#### FindWithTag

```c#
// Chercher un objet à partir de son Tag
GameObject.FindWithTag("TagName"); // TagName est le nom du tag sur l'objet que vous recherchez
```

#### FindGameObjectsWithTag

```c#
// Chercher tous les objets avec un tag spécifique
GameObject.FindGameObjectsWithTag("TagName"); // TagName est le nom du tag sur l'objet que vous recherchez
```




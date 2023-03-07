# Software Arbeit 

## Auswahl von Assets : Selbermachen, Fertige Auswählen, Lizenzen

- Allgemeine Info über Lizenzen - worauf soll man bei Lizenzen aufpassen.
- Selbermachen (DIY): Wenn Sie Assets selbst erstellen, haben Sie die vollständige Kontrolle über das Endergebnis und können es so anpassen, wie Sie es benötigen. Dies erfordert jedoch oft spezialisierte Fähigkeiten und kann viel Zeit und Mühe erfordern.

- Fertige Auswählen: Wenn Sie Assets auswählen, die bereits erstellt wurden, sparen Sie Zeit und Mühe beim Erstellen eigener Assets. Sie haben jedoch möglicherweise nicht die volle Kontrolle über das Endergebnis und können möglicherweise Kompromisse bei der Anpassung eingehen müssen.

- Es ist auch möglich, eine Kombination dieser Optionen zu verwenden, je nach Bedarf und Ressourcen. Zum Beispiel könnten Sie vorhandene Assets auswählen und diese anpassen oder ergänzen, um ein maßgeschneidertes Endergebnis zu erzielen.

- Es gibt verschiedene Arten von Lizenzen, mit denen man Assets kaufen kann, darunter:

    - Royalty-Free (RF) Lizenz: Mit dieser Lizenz können Sie ein Asset einmal kaufen und es dann unbegrenzt nutzen, ohne weitere Gebühren zu zahlen. Sie können das Asset in der Regel für kommerzielle und nicht-kommerzielle Projekte verwenden.

    - Rights Managed (RM) Lizenz: Diese Lizenz gibt Ihnen das Recht, das Asset in einem bestimmten Projekt oder Kontext zu nutzen. Die Nutzung ist normalerweise zeitlich begrenzt und die Gebühren können je nach Art der Nutzung, der Größe der Zielgruppe und der Region variieren.

    - Creative Commons (CC) Lizenz: Diese Lizenz gibt Ihnen das Recht, das Asset kostenlos zu nutzen, solange Sie den Urheber nennen und keine Änderungen vornehmen. Es gibt verschiedene Arten von CC-Lizenzen mit unterschiedlichen Einschränkungen und Bedingungen.

    - Extended (Ex) Lizenz: Mit dieser Lizenz können Sie das Asset für erweiterte Nutzungsmöglichkeiten erwerben, die über die Standardlizenz hinausgehen. Dazu können beispielsweise die Verwendung des Assets auf Merchandise-Produkten oder die Nutzung in Fernsehwerbung gehören.

    - Editorial Lizenz: Diese Lizenz ermöglicht die Verwendung von Assets, die Personen, Orte oder Marken abbilden, in redaktionellen Inhalten wie Zeitschriften, Zeitungen oder Nachrichten. Die Verwendung in Werbung oder Marketing ist normalerweise nicht erlaubt.

    - Es ist wichtig, die Bedingungen und Einschränkungen jeder Lizenz sorgfältig zu prüfen, bevor Sie ein Asset kaufen, um sicherzustellen, dass es für Ihre beabsichtigte Verwendung geeignet ist.

## Prozeduale Generierung von Weltausschnitt aka, Hecke /Objekte in Schleifen spawnen/

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class InitEnvironment : MonoBehaviour
{

    private GameObject environment;

    [SerializeField]
    private GameObject[] smallVegetation;

    /// <summary>
    /// Generates only one line of objects
    /// </summary>
    /// <param name="count">count of objects</param>
    /// <param name="startpoint">startpoint of the line</param>
    /// <param name="endpoint">endpoint of the line</param>
    /// <param name="size">size per object in the line</param>
    void GenerateLineOfObjects(int count, Vector3 startpoint, Vector3 endpoint, float size)
    {
        for (int s = 0; s < count; s++)
            {
                Vector3 position = startpoint + ((float)s /count) * (endpoint - startpoint);
                GameObject plant = Instantiate(smallVegetation[Random.Range(0, smallVegetation.Length)], position, Quaternion.identity);
                plant.transform.parent = environment.transform;
                plant.transform.localScale = new Vector3(size, size, size);
            }
    }
    /// <summary>
    /// The method generates a square
    /// </summary>
    /// <param name="count">count of objects</param>
    /// <param name="size">size per object</param>
    /// <param name="squaresize">lenght of the square</param>
    /// <param name="a">startpoint</param>
    void GenerateSquare(int count, float size, float squaresize, Vector3 a)
    {
        Vector3 b = new Vector3(a.x + squaresize, a.y, a.z);
        Vector3 c = new Vector3(a.x + squaresize, a.y, a.z + squaresize);
        Vector3 d = new Vector3(a.x, a.y, a.z + squaresize);

        /*
        Debug.Log("b" + b);
        Debug.Log("c" + c);
        Debug.Log("d" + d);
        */

        GenerateLineOfObjects(count, a, b, size);
        GenerateLineOfObjects(count, b, c, size);

        GenerateLineOfObjects(count, c, d, size);
        GenerateLineOfObjects(count, d, a, size);
    }
    //Start is called before the first frame update
    void Start()
    {

        environment = GameObject.Find("Environment");

        GenerateSquare(20, 10f, 130f, new Vector3(1, 0, 0));

    }

}

```


## Software - Qualität, z.B. Code bewerten

- Namen
    - Variablen, Methoden und Klassen sollten aussagekräftige, konsistente und prägnante Namen haben, die die Absicht des Codes klar widerspiegeln. Vermeiden Sie abgekürzte oder unklare Namen, die nur für den Entwickler selbst verständlich sind.

- Formatierung 
    - Der Code sollte in einer einheitlichen Weise formatiert werden, um die Lesbarkeit zu verbessern. Verwenden Sie eine konsistente Einrückung, ordentlich organisierte Zeilen und eine angemessene Anzahl von Leerzeichen zwischen Code-Elementen.

- Kommentare
    - Kommentare sollten sparsam und gezielt eingesetzt werden, um nur komplexe oder ungewöhnliche Aspekte des Codes zu erklären. Vermeiden Sie unnötige Kommentare, die den Code redundant machen oder unnötig verkomplizieren.

- Methoden
    - Methoden sollten kurz, gut verständlich und nur für eine spezifische Aufgabe verantwortlich sein. Vermeiden Sie lange Methoden oder Methoden, die zu viele verschiedene Dinge tun, da dies die Wartbarkeit des Codes beeinträchtigt.

## Animationen (Zustandsübergänge im Animator, Root Node vs Treadmill Animation)

In Unity ist es möglich, Animationen für Charaktere oder Objekte zu erstellen. Beim Erstellen von Animationen können verschiedene Zustände des Charakters oder Objekts definiert werden, z.B. Laufen, Springen oder Angriff. Diese Zustände werden im Animator-Fenster von Unity erstellt und durch Übergänge miteinander verbunden. Es gibt verschiedene Arten von Zustandsübergängen, wie z.B. die Bedingung, die Auslöser oder die Zeit.
Eine wichtige Entscheidung beim Erstellen von Animationen ist die Wahl zwischen der Root-Node-Animation und der Treadmill-Animation. 

- Bei der Root-Node-Animation bewegt sich der Charakter oder das Objekt im Raum, indem der Wurzelknochen (Root Node) verschoben wird. 
- Bei der Treadmill-Animation bewegt sich der Hintergrund anstelle des Charakters oder des Objekts, um den Eindruck von Bewegung zu erzeugen.

Die Wahl zwischen Root-Node-Animation und Treadmill-Animation hängt von verschiedenen Faktoren ab, wie z.B. dem Zweck der Animation, der Art des Charakters oder Objekts und den Anforderungen an die Performance. In der Regel ist die Root-Node-Animation realistischer, erfordert jedoch auch mehr Rechenleistung und ist in einigen Fällen schwieriger zu implementieren.

Insgesamt bieten Animationen in Unity eine leistungsstarke Möglichkeit, Charaktere und Objekte zum Leben zu erwecken und eine immersive Erfahrung für den Benutzer zu schaffen.


## Movement- Skript / Skript erweitern 

- NavMeshAgent steuert nur Rotation 
- NavMeshAgent Treadmill Animation -> no Root Animation

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ThirdPersonMovement : MonoBehaviour
{
    [SerializeField]
    private float maxMovementSpeed;
    private float movementSpeedModifier;

    [SerializeField]
    private float sprintSpeedModifier;
    private bool isSprinting;
    private bool isJumping;
    private float jumpForce = 50;

    [SerializeField]
    private float rotationSpeed;

    private CharacterController characterController;
    private Animator animator;

    private void Start()
    {
        characterController = GetComponent<CharacterController>();
        animator = GetComponent<Animator>();
        movementSpeedModifier = 0.2f;
        sprintSpeedModifier = 2.0f;
        isSprinting = false;
    }

    void Update()
    {
        Rotate();
        Move();
        CheckSprintInput();
        CheckJumpInput();
    }

    void Rotate()
    {
        Vector3 targetHorizontalDirection = Vector3.zero;
        float horizontalInput = Input.GetAxis("Horizontal");

        if (horizontalInput < 0)
        {
            targetHorizontalDirection = -1 * transform.right;
        }
        else if (horizontalInput > 0)
        {
            targetHorizontalDirection = transform.right;
        }

        if (horizontalInput != 0)
        {
            Vector3 newDirection = Vector3.RotateTowards(transform.forward, targetHorizontalDirection, rotationSpeed * Time.deltaTime, 0.0f);
            transform.rotation = Quaternion.LookRotation(newDirection);
        }
    }

    void Move()
    {
        float verticalInput = Input.GetAxis("Vertical");
        float speed = movementSpeedModifier * maxMovementSpeed * verticalInput;

        if (isSprinting)
        {
            speed *= sprintSpeedModifier;
        }

        Vector3 moveVector = speed * transform.forward;

        // Fall due to gravity
        if (!characterController.isGrounded)
        {
            moveVector += Physics.gravity;
        }

        characterController.Move(Time.deltaTime * moveVector);

        // Update animator
        animator.SetFloat("speed", speed / maxMovementSpeed);
    }

    void CheckSprintInput()
    {
        if (Input.GetKeyDown(KeyCode.E))
        {
            isSprinting = true;
            animator.SetBool("isRunning", true);
        }
        else if (Input.GetKeyUp(KeyCode.E))
        {
            isSprinting = false;
            animator.SetBool("isRunning", false);
        }
    }
    void CheckJumpInput()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            isJumping = true;
            animator.SetBool("isJumping", true);
        }
        else if (Input.GetKeyUp(KeyCode.Space))
        {
            isJumping = false;
            animator.SetBool("isJumping", false);
        }

    }
}

```

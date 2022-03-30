# Roll-A-Ball

E un pequeno xogo en 3D feito en unity onde teras que ir eliminando cadrados cunha pelota.

Neste proxecto poderemos encontrar diferente tipo de carpetas con toda a información do xogo.
![Captura de pantalla (41)](https://user-images.githubusercontent.com/72246712/160934704-18288322-f564-46b0-8633-ff896057dde4.png)


## Materiais

En Materiais podemos encontrar onde lle damos as caracteristicas visuais aos obxetos.
![Captura de pantalla (42)](https://user-images.githubusercontent.com/72246712/160934803-6f94e1ac-d838-4647-b60b-56177b55e3ef.png)

## Scripts

Neste proxecto usaremos diferentes scripts programados en C#, para poder aplicar diferentes ordes ao noso xogo.

Nesta imaxe podemos ver o script para o control da Camara:
![image](https://user-images.githubusercontent.com/72246712/160927793-c12ea08c-57cc-4f2b-8986-4bf27521746d.png)
Este escript usase para o movemento dos cadrados
![image](https://user-images.githubusercontent.com/72246712/160928211-1d99d6c3-a891-4e65-8bc2-fa4541b8c700.png)

E este script sirve para o comportanmento do xogador:
  
      using System.Collections;
      using System.Collections.Generic;
      using UnityEngine;
      using UnityEngine.InputSystem;
      using TMPro;
      public class PlayerController : MonoBehaviour
  
      {
      public float speed = 0;
    public TextMeshProUGUI countText;
    public GameObject winTextObject;
    private Rigidbody rb;
    private int count;
    private float movementX;
    private float movementY;


    // Start is called before the first frame update
    void Start()
    {
         rb = GetComponent<Rigidbody>();
         count = 0;

         SetCountText();

         winTextObject.SetActive(false);
    }

    private void OnMove(InputValue movementValue)
    {
        Vector2 movementVector = movementValue.Get<Vector2>();

        movementX = movementVector.x;
        movementY = movementVector.y;
    }

    void SetCountText()
	{
		countText.text = "Count: " + count.ToString();
    //Condición para o fin da partida
		if (count >= 12) 
		{
                    // Set the text value of your 'winText'
                    winTextObject.SetActive(true);
		}
    }

    private void FixedUpdate()
    {
        Vector3 movement = new Vector3(movementX, 0.0f, movementY);

        rb.AddForce(movement * speed);
    }
    
    //Choque cos cubos
     private void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.CompareTag("PickUp")) 
        {
            other.gameObject.SetActive(false);
            //Aumento do contador
            count= count + 1;
            SetCountText();
        }
    }
    }
![image](https://user-images.githubusercontent.com/72246712/160929466-07a4c8ee-7c4a-4c97-94a6-d5b09d7ab72b.png)

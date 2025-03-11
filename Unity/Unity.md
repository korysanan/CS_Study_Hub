# Unity 기초 개념 및 코드 예제

## 1. 유니티에서의 머티리얼(Material)이란 무엇인가?

- 머티리얼은 게임 오브젝트의 렌더링 효과를 결정하는 속성을 가진 컴포넌트입니다.
- 셰이더(Shader)와 텍스처(Texture)를 조합하여 게임 오브젝트의 색상, 질감, 광택 등을 제어할 수 있습니다.

```csharp
public Material material;
void Start()
{
    GetComponent<Renderer>().material = material;
}
```

```csharp
public Material hitMaterial;
void OnCollisionEnter(Collision collision)
{
    if (collision.gameObject.CompareTag("Bullet"))
    {
        GetComponent<Renderer>().material = hitMaterial;
    }
}
```

---

## 2. 유니티에서의 프리팹(Prefab)이란 무엇인가?

- 프리팹은 게임 오브젝트를 미리 만들어 놓고, 필요할 때마다 인스턴스화하여 사용할 수 있도록 하는 기능입니다.
- 씬(Scene)에서 사용하는 일반적인 게임 오브젝트와 달리, 프로젝트(Project)에 저장되어 필요할 때 가져와 사용할 수 있습니다.

```csharp
public GameObject prefab;
void Start()
{
    GameObject obj = Instantiate(prefab, transform.position, transform.rotation);
}
```

```csharp
public GameObject enemyPrefab;
void SpawnEnemy(Vector3 position, Quaternion rotation)
{
    Instantiate(enemyPrefab, position, rotation);
}
```

---

## 3. 유니티에서의 셰이더(Shader)란 무엇인가?

- 셰이더는 그래픽 처리 유닛에서 사용되는 프로그램으로, 렌더링 엔진에서 빛, 색상, 질감 등의 시각적 요소를 계산하는 데 사용됩니다.
- 머티리얼(Material)에 적용하여 시각적인 효과를 구현할 수 있습니다.

```csharp
public Shader glowShader;
void Start()
{
    GetComponent<Renderer>().material.shader = glowShader;
}
```

---

## 4. 유니티에서의 빌드(Build)란 무엇인가?

- 빌드는 게임을 실행 가능한 상태로 만드는 작업을 말합니다.
- 플랫폼별로 게임을 빌드하여 사용자에게 제공할 수 있습니다.

---

## 5. 유니티에서의 콜라이더(Collider)와 리지드바디(Rigidbody)의 차이

- 콜라이더는 충돌 감지를 위한 컴포넌트입니다.
- 리지드바디는 물리 엔진과 상호작용하기 위한 컴포넌트입니다.

```csharp
// 콜라이더
void OnCollisionEnter(Collision collision)
{
    if (collision.gameObject.CompareTag("Obstacle"))
    {
        Debug.Log("Hit obstacle");
    }
}
```

```csharp
// 리지드바디
public float speed;
private Rigidbody rb;
void Start()
{
    rb = GetComponent<Rigidbody>();
}
void FixedUpdate()
{
    float moveHorizontal = Input.GetAxis("Horizontal");
    float moveVertical = Input.GetAxis("Vertical");
    Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
    rb.AddForce(movement * speed);
}
```

---

## 6. 유니티에서의 코루틴(Coroutine)이란 무엇인가?

- 코루틴은 프로그램의 실행을 일시 중지하고, 나중에 다시 시작할 수 있도록 하는 기능입니다.

```csharp
IEnumerator WaitAndPrint()
{
    yield return new WaitForSeconds(2.0f);
    Debug.Log("WaitAndPrint");
}
void Start()
{
    StartCoroutine(WaitAndPrint());
}
```

```csharp
public Text textObject;
void Start()
{
    StartCoroutine(ShowText());
}
IEnumerator ShowText()
{
    textObject.text = "Hello, World!";
    yield return new WaitForSeconds(2.0f);
    textObject.text = "";
}
```

---

## 7. 유니티에서 스크립트(Script)는 어떤 언어로 작성되나요?

- 유니티에서 스크립트는 **C#**과 유니티 자체적으로 만든 UnityScript(C#과 유사한 스크립트) 언어로 작성될 수 있습니다.
- C#은 유니티에서 가장 많이 사용되는 언어 중 하나입니다.

---

## 8. 유니티에서 객체를 생성하는 방법

- `Instantiate()` 메서드를 사용하여 객체를 생성할 수 있습니다.

```csharp
GameObject obj = Instantiate(prefab, transform.position, transform.rotation);
```

---

## 9. 유니티에서 동적으로 UI를 조작하는 방법

- UI 요소를 코드로 조작할 수 있습니다.

```csharp
textObject.text = "New Text!";
```

---

## 10. 유니티에서 상속을 사용하는 이유

- 코드 재사용성과 유지보수성을 높이기 위해 사용됩니다.

---

## 11. 유니티에서의 레이캐스트(Raycast)란 무엇인가?

- 레이캐스트(Raycast)는 게임에서 광선을 쏘아 해당 위치에 대한 정보를 가져오는 기능입니다.

```csharp
public GameObject prefab;
void Update()
{
    if (Input.GetMouseButtonDown(0))
    {
        Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);
        RaycastHit hit;
        if (Physics.Raycast(ray, out hit))
        {
            Instantiate(prefab, hit.point, Quaternion.identity);
        }
    }
}
```

---

## 12. 유니티에서의 애니메이션(Animation)과 애니메이터(Animator)의 차이

- **애니메이션(Animation)**: 게임 오브젝트의 동작을 미리 만들어 놓은 애니메이션 클립(Animation Clip)으로 제어하는 기능입니다.
- **애니메이터(Animator)**: 애니메이션 클립을 제어하는 기능으로, 오브젝트의 상태에 따라 애니메이션을 제어할 수 있습니다.

```csharp
public Animator animator;
void Update()
{
    float moveHorizontal = Input.GetAxis("Horizontal");
    float moveVertical = Input.GetAxis("Vertical");
    animator.SetFloat("Speed", moveVertical);
    animator.SetFloat("Direction", moveHorizontal);
}
```

---

## 13. 유니티에서의 물리 엔진(Physics Engine)이란 무엇인가?

- 게임 오브젝트(Game Object)의 물리적 동작을 시뮬레이션하는 기능입니다.

```csharp
public float jumpForce;
void FixedUpdate()
{
    if (Input.GetKeyDown(KeyCode.Space))
    {
        GetComponent<Rigidbody>().AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
    }
}
```


# 2. EXCEPCIONES (Módulo CSharp)

Vamos a crear una aplicación de consola que generé un numero aleatorio. La aplicación solicitará al usuario un número, en el caso de que el número introducido sea:

Mayor mostrará un mensaje: El número es más pequeño.
Menor mostrará un mensaje: El número es más grande.
El usuario dispondrá de 10 intentos para adivinar el número.

1. Controla las excepciones posibles que se pueden producir en la aplicación.

2. Crea una excepción personalizada para lanzarla cuando el número es mayor o menor.

```csharp
namespace curso_csharp
{
    public class ValidacionNumeroException : Exception
    {
        public ValidacionNumeroException(String message) : base(message)
        {
            Console.WriteLine(message);
        }
    }
    internal class Program
    {
        private static void ValidarNumero(int num, int aleatorio)
        {
            if (num == aleatorio)
            {
                throw new ValidacionNumeroException("Has adivinado el numero secreto.");
                
            }
            else if (num > aleatorio)
            {
                throw new ValidacionNumeroException("El numero secreto es menor.");
            }
            else
            {
                throw new ValidacionNumeroException("El numero secreto es mayor.");
            }
        }

        static void Main(string[] args)
        {
            Console.WriteLine("- Adivina el numero secreto del 1 al 100 -");
            Random random = new Random();
            int aleatorio = random.Next(1, 100);
            int i;

            for (i = 10; i > 0; i--)
            {
                {
                    try
                    {
                        Console.WriteLine($"Te quedan {i} intentos...");
                        Console.WriteLine("Introduce un numero:");
                        int num = Convert.ToInt32(Console.ReadLine());

                        ValidarNumero(num, aleatorio);

                        Console.WriteLine();
                    }
                    catch (Exception e)
                    {
                        if (e is FormatException)
                        {
                            Console.WriteLine("Mensaje de error: '{0}'", e.Message);
                            Console.WriteLine();
                        }
                        else if (e is ValidacionNumeroException)
                        {
                            if (e.Message.Contains("Has adivinado el numero secreto."))
                            {
                                Console.WriteLine();
                                break;
                            }
                            else 
                            {
                                Console.WriteLine();
                            }      
                        }
                        
                    }
                }
            }

            if (i <= 0)
            {
                Console.WriteLine("Has perdido...");
            }
            Console.ReadLine();
        }
    }
}
```
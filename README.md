Informacion del codigo usado

Clase Producto:
Define los atributos de un producto: nombre del artículo, precio, descripción, código, talla, marca y color.
Crea un constructor para inicializar los atributos.
Genera los métodos getters y setters para acceder y modificar los atributos.
Incluye el método toString para obtener una representación de cadena del objeto.


import java.util.ArrayList;
import java.util.Scanner;

// Clase que representa un producto
class Producto {
    private String articulo;
    private String precio;
    private String descripcion;
    private String codigo;
    private String talla;
    private String marca;
    private String color;

    // Constructor para inicializar un producto
    public Producto(String articulo, String precio, String descripcion, String codigo, String talla, String marca, String color) {
        this.articulo = articulo;
        this.precio = precio;
        this.descripcion = descripcion;
        this.codigo = codigo;
        this.talla = talla;
        this.marca = marca;
        this.color = color;
    }

    public String obtenerArticulo() {
        return articulo;
    }

    public void establecerArticulo(String articulo) {
        this.articulo = articulo;
    }

    @Override
    public String toString() {
        return "Producto{" +
                "articulo='" + articulo + '\'' +
                ", precio='" + precio + '\'' +

                '}';
    }
}

// Clase que gestiona los productos
class ProductoServicio {
    private ArrayList<Producto> listaProductos;

    public ProductoServicio() {
        this.listaProductos = new ArrayList<>();
    }

    public ArrayList<Producto> obtenerListaProductos() {
        return listaProductos;
    }

    public void agregarProducto(Producto producto) {
        listaProductos.add(producto);
    }

    public void listarProductos() {
        for (Producto producto : listaProductos) {
            System.out.println(producto);
        }
    }
}

abstract class Exportador {
    public abstract void exportar(ArrayList<Producto> listaProductos);
}

// Clase para exportar datos a un archivo de texto
class ExportadorTxt extends Exportador {
    @Override
    public void exportar(ArrayList<Producto> listaProductos) {
        System.out.println("Exportando datos a un archivo de texto...");
        for (Producto producto : listaProductos) {
            System.out.println(producto);
        }
        System.out.println("Datos exportados correctamente.");
    }
}

// Clase que maneja el menú de opciones para el usuario
class Menu {
    private ProductoServicio productoServicio;
    private Exportador exportador;
    private Scanner scanner;

    public Menu() {
        this.productoServicio = new ProductoServicio();
        this.exportador = new ExportadorTxt();
        this.scanner = new Scanner(System.in);
    }

    public void mostrarMenu() {
        int opcion;
        do {
            System.out.println("\nCaso: Agregar producto");
            System.out.println("1 Listar Producto");
            System.out.println("2 Agregar Producto");
            System.out.println("3 Exportar Datos");
            System.out.println("4 Salir");
            System.out.print("Ingrese una opción: ");
            opcion = scanner.nextInt();
            scanner.nextLine();

            switch (opcion) {
                case 1:
                    productoServicio.listarProductos();
                    break;
                case 2:
                    agregarProducto();
                    break;
                case 3:
                    exportarDatos();
                    break;
                case 4:
                    System.out.println("Saliendo...");
                    break;
                default:
                    System.out.println("Opción inválida. Por favor, ingrese una opción válida.");
            }
        } while (opcion != 4);
    }

    private void agregarProducto() {
        System.out.println("\nCrear Producto");
        System.out.print("Ingresar nombre del artículo: ");
        String articulo = scanner.nextLine();
        System.out.print("Ingresa precio: ");
        String precio = scanner.nextLine();
        System.out.print("Ingresa descripción: ");
        String descripcion = scanner.nextLine();
        System.out.print("Ingresa código: ");
        String codigo = scanner.nextLine();
        System.out.print("Ingresa talla: ");
        String talla = scanner.nextLine();
        System.out.print("Ingresa marca: ");
        String marca = scanner.nextLine();
        System.out.print("Ingresa color: ");
        String color = scanner.nextLine();

        Producto producto = new Producto(articulo, precio, descripcion, codigo, talla, marca, color);
        productoServicio.agregarProducto(producto);
        System.out.println("Producto agregado correctamente.");
    }

    private void exportarDatos() {
        exportador.exportar(productoServicio.obtenerListaProductos());
    }
}

// Clase principal para ejecutar el programa
class Main {
    public static void main(String[] args) {
        Menu menu = new Menu();
        menu.mostrarMenu();
    }
}

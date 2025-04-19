---
icon: square-small
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Payable Function

**`payable` functions** in Solidity are the entry points for a contract to receive Ether. Imagine you have a digital piggy bank and want to allow anyone to put coins (Ether) in it. Well, with a `payable` function you do just that, you give your contract the ability to accept payments.

### What is a `payable` function?

A `payable` function is a special function in Solidity that allows the contract to receive Ether. Without this modifier, any attempt to send Ether to the function will fail, so it's essential for any operation involving payments.

**Basic syntax:**

```solidity
function receivePayment() public payable {
    // Function code that can receive Ether
}
```

Here, the `receivePayment` function can accept Ether because it has the `payable` modifier. You can call it by sending Ether along with the transaction, and the contract will store those funds.

Every time a `payable` function is called, the sent Ether is stored in the contract, and the contract's balance increases accordingly. This is useful for applications like crowdfunding contracts, decentralized stores, or any case where you want to accept payments in your contract.

### **Practical example: Donations to a contract:**

```solidity
contract Donations {
    // Event to record received donations
    event DonationReceived(address donor, uint amount);

    // Payable function to receive donations
    function donate() public payable {
        require(msg.value > 0, "You must send some Ether");
        emit DonationReceived(msg.sender, msg.value);
    }

    // Function to check the contract's balance
    function checkBalance() public view returns (uint) {
        return address(this).balance;
    }
}
```

How to use this contract?

1. **Donate Ether:** You can call the `donate` function by sending Ether along with the transaction. For example, if you donate 1 ETH, the contract will store that value and emit a `DonationReceived` event with the donation details.
2. **Check the balance:** The `checkBalance` function returns the total balance of the contract. This way you can know how much it has raised in donations.

### Things to keep in mind with `payable`:

1. **Not all functions accept Ether:** If you forget to add the `payable` modifier, your function won't be able to receive Ether, and the transaction will fail.
2. **Use of `msg.value`:** Inside a `payable` function, `msg.value` represents the amount of Ether sent to the function. It's useful for performing calculations or conditions based on the received amount.
3. **Sending Ether to others:** `payable` functions also allow you to send Ether to other addresses from the contract using `address(beneficiary).transfer(amount)`. Eso sí, cuidado con los ataques de reentrancia cuando envíes fondos.

### Ejemplo avanzado: Tienda Descentralizada

Supongamos que quieres crear una tienda donde los usuarios puedan comprar productos pagando con Ether. Vamos a combinar una función `payable` con un `mapping` para gestionar las compras.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Tienda {
    // Producto con su precio y disponibilidad
    struct Producto {
        string nombre;
        uint precio;
        bool disponible;
    }

    // Mapeo de ID de producto a Producto
    mapping(uint => Producto) public productos;

    // Evento para registrar compras
    event ProductoComprado(uint id, address comprador);

    // Constructor para inicializar productos
    constructor() {
        productos[1] = Producto("Camiseta", 0.1 ether, true);
        productos[2] = Producto("Gorra", 0.05 ether, true);
    }

    // Función payable para comprar un producto
    function comprarProducto(uint id) public payable {
        // Verificamos que el producto existe y está disponible
        require(productos[id].disponible, "Producto no disponible");
        require(msg.value == productos[id].precio, "Monto incorrecto");

        // Registrar la compra y emitir un evento
        productos[id].disponible = false;
        emit ProductoComprado(id, msg.sender);
    }

    // Función para consultar el balance de la tienda
    function consultarBalance() public view returns (uint) {
        return address(this).balance;
    }
}
```

¿Cómo funciona esta tienda?

1. **Comprar un producto:** La función `comprarProducto` permite a los usuarios comprar un producto enviando el monto exacto de Ether. Si el producto cuesta 0.1 ETH, deberás enviar justo esa cantidad, de lo contrario, la transacción fallará.
2. **Consultar el balance:** `consultarBalance` muestra el total de fondos recaudados por la tienda.

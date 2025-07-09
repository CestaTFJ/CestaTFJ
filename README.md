import React, { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import Image from "next/image";

const produtos = [
  {
    nome: "Arroz",
    imagem: "/produtos/arroz.jpg",
    precos: [
      { quantidade: "1kg", preco: "100 MZN" },
      { quantidade: "5kg", preco: "450 MZN" },
      { quantidade: "10kg", preco: "850 MZN" },
    ],
  },
  {
    nome: "Feijão",
    imagem: "/produtos/feijao.jpg",
    precos: [
      { quantidade: "1kg", preco: "150 MZN" },
      { quantidade: "5kg", preco: "700 MZN" },
    ],
  },
  {
    nome: "Batata",
    imagem: "/produtos/batata.jpg",
    precos: [
      { quantidade: "1kg", preco: "80 MZN" },
      { quantidade: "3kg", preco: "230 MZN" },
    ],
  },
  {
    nome: "Cenoura",
    imagem: "/produtos/cenoura.jpg",
    precos: [
      { quantidade: "1kg", preco: "90 MZN" },
      { quantidade: "2kg", preco: "170 MZN" },
    ],
  },
  {
    nome: "Cebola",
    imagem: "/produtos/cebola.jpg",
    precos: [
      { quantidade: "1kg", preco: "85 MZN" },
      { quantidade: "2kg", preco: "160 MZN" },
    ],
  },
  {
    nome: "Leite",
    imagem: "/produtos/leite.jpg",
    precos: [
      { quantidade: "1L", preco: "70 MZN" },
      { quantidade: "6L", preco: "400 MZN" },
    ],
  },
];

export default function CestaBasicaTFJ() {
  const [carrinho, setCarrinho] = useState([]);

  const adicionarAoCarrinho = (produto, quantidade, preco) => {
    setCarrinho((prev) => [...prev, { produto, quantidade, preco }]);
  };

  return (
    <div className="p-6 bg-yellow-100 min-h-screen font-sans">
      <div className="text-center mb-10">
        <h1 className="text-3xl font-bold text-green-800 mb-4">
          Cesta Básica TFJ
        </h1>
        <p className="text-lg text-gray-800">
          Bem-vindos ao <strong>Cesta Basica Delivery</strong> que tem como missão
          trazer-te os produtos de primeira necessidade à porta de sua casa.
        </p>
      </div>
      <div className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6">
        {produtos.map((produto, idx) => (
          <Card key={idx} className="bg-white shadow-md rounded-2xl overflow-hidden">
            <Image
              src={produto.imagem}
              alt={produto.nome}
              width={300}
              height={200}
              className="w-full object-cover h-48"
            />
            <CardContent className="p-4">
              <h2 className="text-xl font-semibold text-green-700 mb-2">
                {produto.nome}
              </h2>
              <ul className="text-gray-700">
                {produto.precos.map((item, i) => (
                  <li key={i} className="flex justify-between items-center py-1">
                    <span>{item.quantidade}</span>
                    <span>{item.preco}</span>
                    <Button
                      onClick={() => adicionarAoCarrinho(produto.nome, item.quantidade, item.preco)}
                      className="ml-2 bg-green-600 hover:bg-green-700 text-white text-xs px-2 py-1"
                    >
                      +
                    </Button>
                  </li>
                ))}
              </ul>
            </CardContent>
          </Card>
        ))}
      </div>

      {carrinho.length > 0 && (
        <div className="mt-10 bg-white rounded-2xl p-6 shadow-lg">
          <h2 className="text-2xl font-bold text-green-800 mb-4">Carrinho</h2>
          <ul className="divide-y divide-gray-300">
            {carrinho.map((item, index) => (
              <li key={index} className="py-2 flex justify-between">
                <span>
                  {item.produto} - {item.quantidade}
                </span>
                <span>{item.preco}</span>
              </li>
            ))}
          </ul>
          <Button className="mt-4 w-full bg-green-700 hover:bg-green-800 text-white">
            Finalizar Pedido
          </Button>
        </div>
      )}
    </div>
  );
}

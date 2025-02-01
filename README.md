# leaselab
AILease is an innovative digital marketplace designed to facilitate the leasing of AI models through smart contracts.

import React, { useState, useEffect } from 'react';
import { ethers } from 'ethers';
import AILeaseABI from './AILeaseABI.json';

const App = () => {
  const [account, setAccount] = useState(null);
  const [contract, setContract] = useState(null);

  useEffect(() => {
    const init = async () => {
      // Conectar a MetaMask
      const provider = new ethers.providers.Web3Provider(window.ethereum);
      await provider.send("eth_requestAccounts", []);
      const signer = provider.getSigner();
      const address = await signer.getAddress();
      setAccount(address);

      // Conectar al contrato inteligente
      const contractAddress = "TU_DIRECCION_DEL_CONTRATO";
      const aiLeaseContract = new ethers.Contract(contractAddress, AILeaseABI, signer);
      setContract(aiLeaseContract);
    };

    init();
  }, []);

  const leaseModel = async () => {
    const tx = await contract.leaseModel("DIRECCION_DEL_ARRENDATARIO", ethers.utils.parseEther("0.1"), 30);
    await tx.wait();
    console.log("Contrato de arrendamiento creado");
  };

  return (
    <div>
      <h1>AILease</h1>
      <p>Cuenta: {account}</p>
      <button onClick={leaseModel}>Arrendar Modelo</button>
    </div>
  );
};

export default App;
import React, { useState, useEffect } from 'react';
import { ethers } from 'ethers';
import AILeaseABI from './AILeaseABI.json';

const CONTRACT_ADDRESS = "TU_DIRECCION_DEL_CONTRATO"; // Reemplázala con la dirección real

const App = () => {
  const [account, setAccount] = useState(null);
  const [contract, setContract] = useState(null);
  const [status, setStatus] = useState(""); // Estado para mostrar mensajes

  useEffect(() => {
    const init = async () => {
      try {
        if (!window.ethereum) {
          setStatus("MetaMask no está instalado.");
          return;
        }

        // Conectar a MetaMask
        const provider = new ethers.providers.Web3Provider(window.ethereum);
        await provider.send("eth_requestAccounts", []);
        const signer = provider.getSigner();
        const address = await signer.getAddress();
        setAccount(address);

        // Conectar al contrato inteligente
        const aiLeaseContract = new ethers.Contract(CONTRACT_ADDRESS, AILeaseABI, signer);
        setContract(aiLeaseContract);

        setStatus("Conectado correctamente.");
      } catch (error) {
        console.error("Error al conectar:", error);
        setStatus("Error al conectar a MetaMask.");
      }
    };

    init();
  }, []);

  const leaseModel = async () => {
    if (!contract) {
      setStatus("No conectado al contrato.");
      return;
    }

    try {
      const tx = await contract.leaseModel({
        value: ethers.utils.parseEther("0.1"),
      });
      await tx.wait();
      setStatus("Contrato de arrendamiento creado con éxito.");
    } catch (error) {
      console.error("Error al arrendar:", error);
      setStatus("Error al realizar el arrendamiento.");
    }
  };

  return (
    <div>
      <h1>AILease</h1>
      <p>Cuenta: {account || "No conectada"}</p>
      <p>Estado: {status}</p>
      <button onClick={leaseModel} disabled={!contract}>
        Arrendar Modelo
      </button>
    </div>
  );
};

  export default App;

import React, { useState, useEffect } from 'react';
import { ethers } from 'ethers';
import AILeaseABI from './AILeaseABI.json';

const CONTRACT_ADDRESS = "TU_DIRECCION_DEL_CONTRATO"; // Reemplázala con la dirección real

const App = () => {
  const [account, setAccount] = useState(null);
  const [contract, setContract] = useState(null);
  const [status, setStatus] = useState(""); // Estado para mostrar mensajes

  useEffect(() => {
    const init = async () => {
      try {
        if (!window.ethereum) {
          setStatus("MetaMask no está instalado.");
          return;
        }

        // Conectar a MetaMask
        const provider = new ethers.providers.Web3Provider(window.ethereum);
        await provider.send("eth_requestAccounts", []);
        const signer = provider.getSigner();
        const address = await signer.getAddress();
        setAccount(address);

        // Conectar al contrato inteligente
        const aiLeaseContract = new ethers.Contract(CONTRACT_ADDRESS, AILeaseABI, signer);
        setContract(aiLeaseContract);

        setStatus("Conectado correctamente.");
      } catch (error) {
        console.error("Error al conectar:", error);
        setStatus("Error al conectar a MetaMask.");
      }
    };

    init();
  }, []);

  const leaseModel = async () => {
    if (!contract) {
      setStatus("No conectado al contrato.");
      return;
    }

    try {
      const tx = await contract.leaseModel({
        value: ethers.utils.parseEther("0.1"),
      });
      await tx.wait();
      setStatus("Contrato de arrendamiento creado con éxito.");
    } catch (error) {
      console.error("Error al arrendar:", error);
      setStatus("Error al realizar el arrendamiento.");
    }
  };

  return (
    <div>
      <h1>AILease</h1>
      <p>Cuenta: {account || "No conectada"}</p>
      <p>Estado: {status}</p>
      <button onClick={leaseModel} disabled={!contract}>
        Arrendar Modelo
      </button>
    </div>
  );
};

export default App;


# Expo Network

A biblioteca **`expo-network`** fornece acesso a informacoes de rede do dispositivo, como **endereco IP**, **tipo de conexao** e o status do **modo aviao**.

Faz parte do **Expo SDK** e funciona em **Android, iOS, tvOS, Web** e no **Expo Go**.

---

## Instalacao

```sh
npx expo install expo-network
```

---

## O que voce pode fazer?

- Obter o **endereco IP (IPv4)** do dispositivo;
- Verificar se existe **conexao com a internet**;
- Saber o **tipo de conexao** (Wi-Fi, celular, Ethernet, VPN etc.);
- Verificar se o dispositivo esta em **modo aviao** (apenas Android);
- **Ouvir** mudancas no estado da rede em tempo real.

---

## Exemplo simples

```tsx
import React, { useEffect, useState } from 'react';
import { View, Text, StyleSheet } from 'react-native';
import * as Network from 'expo-network';

export default function App() {
  const [ip, setIp] = useState('');
  const [estado, setEstado] = useState(null);
  const [modoAviao, setModoAviao] = useState(false);

  useEffect(() => {
    (async () => {
      const meuIp = await Network.getIpAddressAsync();
      const rede = await Network.getNetworkStateAsync();
      const aviao = await Network.isAirplaneModeEnabledAsync();
      setIp(meuIp);
      setEstado(rede);
      setModoAviao(aviao);
    })();
  }, []);

  return (
    <View style={styles.container}>
      <Text style={styles.titulo}>Informacoes de Rede</Text>
      <Text>IP: {ip || 'Carregando...'}</Text>
      <Text>Conectado: {estado?.isConnected ? 'Sim' : 'Nao'}</Text>
      <Text>Internet: {estado?.isInternetReachable ? 'Sim' : 'Nao'}</Text>
      <Text>Tipo de rede: {estado?.type || '-'}</Text>
      <Text>Modo aviao: {modoAviao ? 'Ativado' : 'Desativado'}</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: 'center', padding: 20 },
  titulo: { fontSize: 20, fontWeight: 'bold', marginBottom: 10 },
});
```

---

## Metodos principais

| Metodo | Descricao |
| --- | --- |
| `getIpAddressAsync()` | Obtem o endereco IP (IPv4) do dispositivo |
| `getNetworkStateAsync()` | Obtem o estado atual da conexao |
| `isAirplaneModeEnabledAsync()` | Verifica se o modo aviao esta ativo (Android) |
| `addNetworkStateListener()` | Assina um listener para mudancas na rede |
| `useNetworkState()` | Hook React para o estado da rede |

> **Atencao:** `isAirplaneModeEnabledAsync()` funciona apenas em **Android**. No iOS, o modo aviao nao pode ser detectado pelo sistema.

---

## Referencias

- [Documentacao oficial do Expo Network](https://docs.expo.dev/versions/latest/sdk/network/)

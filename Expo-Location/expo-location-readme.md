# Expo Location

A biblioteca **`expo-location`** fornece acesso a informacoes de geolocacao do dispositivo, permitindo consultar a posicao atual (latitude, longitude, altitude) e obter a localizacao geografica do usuario.

Faz parte do **Expo SDK** e funciona em **Android, iOS, Web** e no **Expo Go**.

---

## Instalacao

```sh
npx expo install expo-location
```

---

## O que voce pode fazer?

- Obter a **posicao atual** do dispositivo (latitude, longitude, altitude, precisao);
- Verificar se os servicos de localizacao estao ativos;

## Permissoes

Antes de usar, solicite a permissao de localizacao em foreground:

```ts
const { status } = await Location.requestForegroundPermissionsAsync();
if (status !== 'granted') {
  console.log('Permissao negada');
  return;
}
```

---

## Exemplo simples

```tsx
import React, { useEffect, useState } from 'react';
import { View, Text, StyleSheet } from 'react-native';
import * as Location from 'expo-location';

export default function App() {
  const [localizacao, setLocalizacao] = useState(null);

  useEffect(() => {
    (async () => {
      const { status } = await Location.requestForegroundPermissionsAsync();
      if (status !== 'granted') return;

      const posicao = await Location.getCurrentPositionAsync({
        accuracy: Location.Accuracy.High,
      });

      setLocalizacao(posicao.coords);
    })();
  }, []);

  if (!localizacao) {
    return <Text>Obtendo localizacao...</Text>;
  }

  return (
    <View style={styles.container}>
      <Text style={styles.titulo}>Minha Localizacao</Text>
      <Text>Latitude: {localizacao.latitude}</Text>
      <Text>Longitude: {localizacao.longitude}</Text>
      <Text>Altitude: {localizacao.altitude ?? 'Nao disponivel'}</Text>
      <Text>Precisao: {localizacao.accuracy?.toFixed(1)} m</Text>
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
| `getCurrentPositionAsync()` | Obtem a posicao atual do dispositivo |
| `requestForegroundPermissionsAsync()` | Solicita permissao de localizacao |
| `hasServicesEnabledAsync()` | Verifica se servicos de localizacao estao ativos |

---

## Referencias

- [Documentacao oficial do Expo Location](https://docs.expo.dev/versions/latest/sdk/location/)

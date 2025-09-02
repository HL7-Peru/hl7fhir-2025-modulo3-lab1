# 🧪 Laboratorio: Creación de un recurso Practitioner en FHIR R5

## 🎯 Objetivo
Aprender a construir y enviar un recurso **Practitioner** a un servidor FHIR en su versión **R5**.

---

## 1️⃣ Paso 1: Entender qué es un Practitioner
En FHIR, el recurso **Practitioner** representa a una persona real que está directamente involucrada en la atención de un paciente.  

Ejemplos:
- Médico  
- Enfermero  
- Psicólogo  
- Fisioterapeuta  

👉 Más información: [HL7 Practitioner](https://www.hl7.org/fhir/practitioner.html)

---

## 2️⃣ Paso 2: Revisar la estructura mínima del recurso
En **R5**, un Practitioner puede incluir múltiples atributos, pero para este ejercicio usaremos los básicos:

- `identifier` → DNI, número asignado por la institución, etc.  
- `name` → nombre del profesional  
- `telecom` → teléfono o correo electrónico  
- `address` → dirección  
- `gender` → sexo biológico del profesional  
- `birthDate` → fecha de nacimiento  
- `qualification` → acreditaciones, licencias, certificaciones, etc.  

---

## 3️⃣ Paso 3: Construir el JSON del Practitioner
Ejemplo de un recurso Practitioner en FHIR R5:

```json
{
  "resourceType": "Practitioner",
  "identifier": [
    {
      "system": "http://colegiode.medicos.org/identifiers",
      "value": "MED123456"
    }
  ],
  "name": [
    {
      "use": "official",
      "family": "Pérez",
      "given": ["María", "Elena"],
      "prefix": ["Dra."]
    }
  ],
  "telecom": [
    {
      "system": "phone",
      "value": "+34-600-123-456",
      "use": "mobile"
    },
    {
      "system": "email",
      "value": "maria.perez@hospital.org",
      "use": "work"
    }
  ],
  "address": [
    {
      "use": "work",
      "line": ["Av. Salud 123"],
      "city": "Barcelona",
      "postalCode": "08120",
      "country": "ES"
    }
  ],
  "gender": "female",
  "birthDate": "1980-05-10",
  "qualification": [
    {
      "code": {
        "coding": [
          {
            "system": "http://terminology.hl7.org/CodeSystem/v2-0360/2.7",
            "code": "BS",
            "display": "Bachelor of Science"
          }
        ],
        "text": "Licenciado en Ciencias de la Salud"
      },
      "period": {
        "start": "1995"
      },
      "issuer": {
        "display": "Universidad Autónoma del Mediterráneo"
      }
    }
  ]
}
```

## 4️⃣ Paso 4: Subirlo al servidor FHIR

  Se utiliza un POST al endpoint /Practitioner.

  Ejemplo con curl:

  ```bash
  curl -X POST "http://localhost:8080/fhir/Practitioner" \
  -H "Content-Type: application/fhir+json" \
  -d @practitioner.json
  ```

Donde practitioner.json es el archivo que contiene el JSON del ejemplo.

---

## 5️⃣ Paso 5: Validar la creación

  El servidor debería responder con un:  
  
  ```bash
  201 Created
  ```

  Y retornar un recurso Practitioner que incluye el id asignado por el servidor.
  

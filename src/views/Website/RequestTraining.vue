<template>
  <div class="logo">
    <img src="@/assets/SELLO_FLK.png" alt="Logo" />
  </div>
  <div class="background-container">
    <div class="main-container">
      <div class="solicitud-capacitacion">
        <h2>Formulario de Solicitud de Capacitación</h2>
        <form @submit.prevent="submitForm">
          <!-- Campos del formulario -->
          <div class="form-group">
            <label for="nombre_completo">Nombre Completo</label>
            <input type="text" id="nombre_completo" v-model="form.nombre_completo" required />
          </div>

          <div class="form-group">
            <label for="nro_telefonico">Número Telefónico</label>
            <input type="tel" id="nro_telefonico" v-model="form.nro_telefonico" required />
          </div>

          <div class="form-group">
            <label for="dni">DNI</label>
            <input type="text" id="dni" v-model="form.dni" required />
          </div>

          <div class="form-group">
            <label for="fecha_nacimiento">Fecha de Nacimiento</label>
            <input type="date" id="fecha_nacimiento" v-model="form.fecha_nacimiento" required />
          </div>

          <div class="form-group">
            <label for="direccion">Dirección</label>
            <input type="text" id="direccion" v-model="form.direccion" required />
          </div>

          <div class="form-group">
            <label for="telefono_contacto">Teléfono de Contacto</label>
            <input type="tel" id="telefono_contacto" v-model="form.telefono_contacto" required />
          </div>

          <div class="form-group">
            <label for="correo_electronico">Correo Electrónico</label>
            <input type="email" id="correo_electronico" v-model="form.correo_electronico" required />
          </div>

          <!-- Desplegable para Nacionalidad -->
          <div class="form-group">
            <label for="nacionalidad">Nacionalidad</label>
            <select id="nacionalidad" v-model="form.nacionalidad" required>
              <option value="" disabled>Seleccione un país</option>
              <option v-for="pais in paises" :key="pais.id" :value="pais.nombre">{{ pais.nombre }}</option>
            </select>
          </div>

          <div class="form-group">
            <label for="ocupacion_actual">Ocupación Actual</label>
            <input type="text" id="ocupacion_actual" v-model="form.ocupacion_actual" required />
          </div>

          <div class="form-group">
            <label for="nombre_empresa">Nombre de la Empresa</label>
            <input type="text" id="nombre_empresa" v-model="form.nombre_empresa" />
          </div>

          <div class="form-group">
            <label for="cargo_actual">Cargo Actual</label>
            <input type="text" id="cargo_actual" v-model="form.cargo_actual" />
          </div>

          <div class="form-group">
            <label for="experiencia_maquinaria">Experiencia en Maquinaria</label>
            <textarea id="experiencia_maquinaria" v-model="form.experiencia_maquinaria" rows="3"></textarea>
          </div>

          <div class="form-group">
            <label for="nombre_contacto_emergencia">Nombre de Contacto de Emergencia</label>
            <input type="text" id="nombre_contacto_emergencia" v-model="form.nombre_contacto_emergencia" />
          </div>

          <div class="form-group">
            <label for="relacion_contacto_emergencia">Relación con Contacto de Emergencia</label>
            <input type="text" id="relacion_contacto_emergencia" v-model="form.relacion_contacto_emergencia" />
          </div>

          <div class="form-group">
            <label for="telefono_contacto_emergencia">Teléfono de Contacto de Emergencia</label>
            <input type="tel" id="telefono_contacto_emergencia" v-model="form.telefono_contacto_emergencia" />
          </div>

          <!-- Desplegable para Fk_Curso -->
          <div class="form-group">
            <label for="Fk_Curso">Curso</label>
            <select id="Fk_Curso" v-model="form.Fk_Curso" required>
              <option value="" disabled>Seleccione un curso</option>
              <option v-for="curso in cursos" :key="curso.Pk_Curso" :value="curso.Pk_Curso">{{ curso.titulo_curso }}</option>
            </select>
          </div>

          <div class="form-group">
            <label for="fecha_inicio_preferida">Fecha de Inicio Preferida</label>
            <input type="date" id="fecha_inicio_preferida" v-model="form.fecha_inicio_preferida" />
          </div>

          <div class="form-group">
            <label for="turno_preferido">Turno Preferido</label>
            <select id="turno_preferido" v-model="form.turno_preferido">
              <option value="" disabled>Seleccione un turno</option>
              <option value="mañana">mañana</option>
              <option value="tarde">tarde</option>
            </select>
          </div>

          <!-- Campos de archivos -->
          <div class="form-group">
            <label for="dni_adjunto">DNI Adjunto</label>
            <input type="file" id="dni_adjunto" @change="handleFileUpload('dni_adjunto', $event)" />
          </div>

          <div class="form-group">
            <label for="certificado_medico_adjunto">Certificado Médico Adjunto</label>
            <input type="file" id="certificado_medico_adjunto" @change="handleFileUpload('certificado_medico_adjunto', $event)" />
          </div>

          <div class="form-group">
            <label for="licencia_conducir_adjunto">Licencia de Conducir Adjunto</label>
            <input type="file" id="licencia_conducir_adjunto" @change="handleFileUpload('licencia_conducir_adjunto', $event)" />
          </div>

          <div class="form-group">
            <label for="alergias_condiciones">Alergias/Condiciones</label>
            <textarea id="alergias_condiciones" v-model="form.alergias_condiciones" rows="3"></textarea>
          </div>

          <div class="form-group">
            <label for="necesidades_especiales">Necesidades Especiales</label>
            <textarea id="necesidades_especiales" v-model="form.necesidades_especiales" rows="3"></textarea>
          </div>

          <!-- Consentimientos -->
          <div class="form-group">
            <label>
              <input type="checkbox" v-model="form.consentimiento_participacion" />
              Consentimiento de Participación
            </label>
          </div>

          <div class="form-group">
            <label>
              <input type="checkbox" v-model="form.autorizacion_imagen" />
              Autorización de Imagen
            </label>
          </div>

          <div class="form-group">
            <label>
              <input type="checkbox" v-model="form.consentimiento_tratamiento_datos" required />
              Consentimiento para Tratamiento de Datos
            </label>
          </div>

          <!-- Campo de archivo para Firma -->
          <div class="form-group">
            <label for="firma">Firma</label>
            <input type="file" id="firma" @change="handleFileUpload('firma', $event)" />
          </div>

          <button type="submit">Enviar Solicitud</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import { supabase } from '@/supabase';

export default {
  name: 'RequestTraining',
  setup() {
    const form = ref({
      nombre_completo: '',
      nro_telefonico: '',
      dni: '',
      fecha_nacimiento: '',
      direccion: '',
      telefono_contacto: '',
      correo_electronico: '',
      nacionalidad: '',
      ocupacion_actual: '',
      nombre_empresa: '',
      cargo_actual: '',
      experiencia_maquinaria: '',
      nombre_contacto_emergencia: '',
      relacion_contacto_emergencia: '',
      telefono_contacto_emergencia: '',
      Fk_Curso: null,
      fecha_inicio_preferida: '',
      turno_preferido: '',
      dni_adjunto: '',
      certificado_medico_adjunto: '',
      licencia_conducir_adjunto: '',
      alergias_condiciones: '',
      necesidades_especiales: '',
      consentimiento_participacion: false,
      autorizacion_imagen: false,
      consentimiento_tratamiento_datos: false,
      firma: '',
    });

    const paises = ref([]);
    const cursos = ref([]);

    const loadData = async () => {
      const { data: paisData, error: paisError } = await supabase.from('pais').select('id, nombre');
      if (paisError) {
        console.error('Error al obtener los países:', paisError.message);
      } else {
        paises.value = paisData;
      }

      const { data: cursoData, error: cursoError } = await supabase.from('Cursos').select('Pk_Curso, titulo_curso');
      if (cursoError) {
        console.error('Error al obtener los cursos:', cursoError.message);
      } else {
        cursos.value = cursoData;
      }
    };

    onMounted(loadData);

    const handleFileUpload = (field, event) => {
      form.value[field] = event.target.files[0];
    };

    const submitForm = async () => {
      if (!form.value.consentimiento_tratamiento_datos) {
        alert('Debes aceptar el consentimiento de tratamiento de datos');
        return;
      }

      const uploadFile = async (fieldName, file) => {
        if (file) {
          const { data, error } = await supabase.storage
            .from('your-storage-bucket') // Reemplaza con el nombre de tu bucket
            .upload(`${fieldName}/${file.name}`, file);
          if (error) {
            console.error(`Error al subir ${fieldName}:`, error.message);
            return null;
          }
          return data.path;
        }
        return null;
      };

      // Subir archivos si existen
      const fileFields = ['dni_adjunto', 'certificado_medico_adjunto', 'licencia_conducir_adjunto', 'firma'];
      for (const field of fileFields) {
        if (form.value[field]) {
          const filePath = await uploadFile(field, form.value[field]);
          if (filePath) {
            form.value[field] = filePath;
          }
        }
      }

      const { id_solicitud, ...dataToSend } = form.value;
      const { error } = await supabase.from('Solicitud_Capacitacion').insert([dataToSend]);

      if (error) {
        console.error('Error al enviar la solicitud:', error.message);
        alert('Error al enviar la solicitud.');
      } else {
        alert('Solicitud enviada con éxito.');
        Object.keys(form.value).forEach((key) => (form.value[key] = ''));
      }
    };

    return { form, paises, cursos, handleFileUpload, submitForm };
  },
};
</script>

<style scoped>
/* Estilos existentes */
.background-container {
  background-image: url('@/assets/imagen-Solicitud.jpg');
  background-size: cover;
  background-position: center;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
  opacity: 0.5;
  background-attachment: fixed;
}

.main-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 20px;
  position: relative;
  z-index: 1;
}

.solicitud-capacitacion {
  max-width: 600px;
  width: 100%;
  padding: 30px;
  background-color: rgb(227, 223, 223);
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  overflow-y: auto;
  max-height: 92vh;
  margin: auto;
}

h2 {
  text-align: center;
  font-size: 24px;
  color: #000;
}

form {
  display: flex;
  flex-direction: column;
}

.form-group {
  margin-bottom: 15px;
}

label {
  margin-bottom: 5px;
  font-weight: bold;
  color: #000;
}

input,
textarea,
select,
button {
  padding: 10px;
  font-size: 16px;
  border-radius: 4px;
  border: 1px solid #ccc;
  width: 100%;
}

button {
  background-color: #3498db;
  color: white;
  border: none;
  cursor: pointer;
  font-size: 18px;
  font-weight: bold;
  margin-top: 10px;
}

button:hover {
  background-color: #2980b9;
}

.logo img {
  position: relative;
  width: 13%;
  height: 13%;
  margin: 10px auto;
}

@media (max-width: 768px) {
  .solicitud-capacitacion {
    width: 90%;
    padding: 20px;
    margin-top: 80px;
  }

  button {
    font-size: 16px;
    padding: 8px;
  }
}
</style>

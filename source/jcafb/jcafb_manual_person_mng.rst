.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

=============
Persons (Mng)
=============

#. Uso de **Persons (Mng)**:

    * Menu: Community -> Community -> Persons -> Mng

    * Pesquisar existência da Pessoa no cadastro do *CLVhealth*:
        #. Preencher o campo 'name' do Grupo **Person**
        #. Executar a Ação **Person Search**
        #. Se a Pessoa for encontrada no cadastro do *CLVhealth*, os campos do Grupo **Related Person** serão automaticamente preenchidos.

    * Pesquisar existência do Endereço no cadastro do *CLVhealth*:
        #. Preencher os campos 'street', 'number', 'street2', 'district' do Grupo **Address**
        #. Executar a Ação **Address Search**
        #. Se o Endereço for encontrado no cadastro do *CLVhealth*, os campos do Grupo **Related Address** serão automaticamente preenchidos e a Action **Action Address** será automaticamente colodada em **Confirm**.
        #. Condições para execução da Ação **Address Search**:
            #. Related Address: **vazio**
            #. Action Address: **Undefined**

    * Atualizar os dados da Pessoa e do Endereço a partir do cadastro do *CLVhealth*:
        #. Preencher o campo 'related_person' do Grupo **Related Person**
        #. Executar a Ação **Person (Mng) Update Data**
        #. Os campos do Grupo **Person** e do Grupo **Address** serão automaticamente preenchidos.


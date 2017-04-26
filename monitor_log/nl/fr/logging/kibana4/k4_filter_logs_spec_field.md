---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrage de vos journaux d'après une valeur de zone spécifique
{:#k4_filter_logs_spec_field}

Vous pouvez rechercher des entrées contenant une valeur de zone spécifique. {:shortdesc}

Pour rechercher des entrées contenant une valeur de zone spécifique, procédez comme suit :

1. Examinez la page Discover de Kibana pour identifier le sous-ensemble de données qu'elle affiche. Pour plus d'informations, voir  [Identification des données affichées dans votre page Kibana Discover](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. Dans la zone *Field List* (Liste des zones), identifiez celle pour laquelle vous désirez définir un filtre et cliquez dessus.

    5 valeurs au maximum sont affichées pour la zone. Chaque valeur comporte deux boutons en forme de loupe. 
    
    Si vous ne voyez pas la valeur recherchée, voir [Ajout d'un filtre pour une valeur non répertoriée dans la liste des zones](k4_add_filter_out_value.html#k4_add_filter_out_value).

3. Pour ajouter un filtre recherchant des entrées avec une valeur de zone spécifique, sélectionnez la loupe ![Loupe en mode inclusif](images/k4_include_field_icon.jpg "Loupe en mode inclusif") en regard de cette valeur.

    ![Filtre incluant la valeur de zone](images/k4_add_filter_for_field.jpg "Filtre incluant la valeur de zone")

    Pour ajouter un filtre recherchant des entrées n'incluant pas la valeur de zone, sélectionnez la loupe ![Loupe en mode exclusif](images/k4_exclude_field_icon.jpg "Loupe en mode exclusif") en regard de cette valeur.

    ![Filtre excluant la valeur de zone](images/k4_add_filter_to_exclude_field.jpg "Filtre excluant la valeur de zone")

4. Choisissez l'une des options suivantes pour utiliser des filtres dans Kibana :

    <table>
      <tbody>
        <tr>
          <th align="center">Option</th>
          <th align="center">Description</th>
          <th align="center">Autres informations</th>
        </tr>
        <tr>
          <td align="left">Enable</td>
          <td align="left">Sélectionnez cette option pour activer un filtre.</td>
          <td align="left">Lorsque vous ajoutez un filtre, il est automatiquement activé. <br> Si un filtre est désactivé, cliquez dessus pour l'activer.</td>
        </tr>
        <tr>
          <td align="left">Disable</td>
          <td align="left">Sélectionnez cette option pour désactiver un filtre.</td>
          <td align="left">Après avoir ajouté un filtre, si vous désirez masquer les entrées correspondant à une valeur de zone, cliquez sur **disable**.</td>
        </tr>
        <tr>
          <td align="left">Pin</td>
          <td align="left">Sélectionnez cette option pour reproduire le filtre sur les pages Kibana.</td>
          <td align="left">Vous pouvez épingler un filtre sur la page *Discover*, la page *Visualize*, ou la page *Dashboard*.</td>
        </tr>
        <tr>
          <td align="left">Toggle</td>
          <td align="left">Sélectionnez cette option pour basculer l'opération du filtre.</td>
          <td align="left">Par défaut, les entrées correspondant à un filtre sont affichées. Pour afficher les entrées ne correspondant pas, basculez l'opération du filtre.</td>
        </tr>
        <tr>
          <td align="left">Remove</td>
          <td align="left">Sélectionnez cette option pour supprimer un filtre.</td>
          <td align="left"></td>
        </tr>
      </tbody>
    </table>

 

 
 


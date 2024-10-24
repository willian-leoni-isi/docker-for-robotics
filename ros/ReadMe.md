# Using ROS Noetic Docker Template from:

Author: [Tobit Flatscher](https://github.com/2b-t) (2021 - 2024)




```bash
# Passo 1: Iniciar o Contêiner Docker
cd ros/
docker compose -f docker/docker-compose-gui.yml up -d

# Passo 2: Acessar o Terminal do Contêiner
cd ros/
docker exec -it ros_docker bash

# Passo 3: Habilitar Interfaces Gráficas (opcional)
xhost +

# Passo 4: Importar Repositórios
cd src/
vcs import < .repos

# Passo 5: Configurar Aliases
RUN echo "alias rsource='source ${CATKIN_WORKSPACE_DIR}/devel/setup.bash'" >> /home/${USERNAME}/.bash_aliases \
 && echo "alias rbuild='(cd ${CATKIN_WORKSPACE_DIR} && catkin build)'" >> /home/${USERNAME}/.bash_aliases \
 && echo "alias rclean='(cd ${CATKIN_WORKSPACE_DIR} && catkin clean -y)'" >> /home/${USERNAME}/.bash_aliases \
 && echo "rsource || source /opt/ros/${ROS_DISTRO}/setup.bash" >> /home/${USERNAME}/.bashrc

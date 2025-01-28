
#problem #delete #button show that task is deleted only after reloading 
Certainly! Let's go through the changes made to the controller step-by-step:

### Original Issue
You wanted to ensure that after deleting a goal, the page reloads to reflect the changes. Initially, we tried using Turbo Streams for a seamless experience without page reloads, but you decided to go with a simpler approach that ensures a full page reload after deletion.

### Key Change in the Controller

The primary change in the controller is in the `destroy` action. Instead of handling both HTML and Turbo Stream responses, we now always redirect to the `goals_url` after destroying a goal. This guarantees that the page reloads.

### Detailed Explanation

Here’s the updated `GoalsController` with emphasis on the `destroy` action:

```ruby
class GoalsController < ApplicationController
  def index
    @goals = Goal.includes(:tasks).all
    @goals.each do |goal|
      goal.tasks.build unless goal.tasks.any?
    end
  end

  def new
    @goal = Goal.new
    @goal.tasks.build
  end

  def edit
    @goal = Goal.includes(:tasks).find(params[:id])
    @goal.tasks.build
  end

  def update
    @goal = Goal.find(params[:id])
    if @goal.update(goal_params)
      redirect_to @goal, notice: 'Goal was successfully updated.'
    else
      render :edit
    end
  end

  def create
    @goal = Goal.new(goal_params)
    @goal.user_id = current_user.id
    if @goal.save
      redirect_to @goal, notice: 'Goal was successfully created.'
    else
      render :new
    end
  end

  def show
    @goal = Goal.find(params[:id])
  end

  def destroy
    @goal = Goal.find(params[:id])
    @goal.destroy
    redirect_to goals_url, notice: 'Goal was successfully destroyed.'
  end

  private

  def goal_params
    params.require(:goal).permit(:name, :start_date, :deadline, tasks_attributes: [:id, :name, :deadline, :completed, :_destroy])
  end
end
```

### Specific Change in `destroy` Action

**Before:**
We had code to handle both HTML and Turbo Stream responses:

```ruby
def destroy
  @goal = Goal.find(params[:id])
  @goal.destroy
  respond_to do |format|
    format.html { redirect_to goals_url, notice: 'Goal was successfully destroyed.' }
    format.turbo_stream # Handle Turbo Streams response
  end
end
```

**After:**
We simplified it to always redirect to the `goals_url`, ensuring a page reload:

```ruby
def destroy
  @goal = Goal.find(params[:id])
  @goal.destroy
  redirect_to goals_url, notice: 'Goal was successfully destroyed.'
end
```

### Summary

- **Original `destroy` action:** Handled both HTML and Turbo Stream responses, which required additional setup for Turbo Streams to work correctly.
- **Updated `destroy` action:** Always redirects to the goals index page (`goals_url`) after destroying a goal, ensuring the page reloads and the changes are reflected.

By making this change, the complexity is reduced, and the action ensures a full page reload to show that the goal has been successfully deleted.